
(function(){


window.buildShader = function(nodeList){
	//this._particleState.animNodes;
	var shader_methods = getAllShaderList(nodeList)
	var _passUsage = phaseEnd({}, shader_methods);
	
	var dest = build(_passUsage.vertexShader);
	var dest_fs = build(_passUsage.fragmentShader);
}


function getAllShaderList(nodeList) {
	var _vs_shader_methods = {};
	var _fs_shader_methods = {};
	for (var node of nodeList){
		var shaderName = node.vertex_ShaderName;
		console.log(shaderName);
		console.log(node.name);
		
		for (var ShaderPhase in shaderName) {
			if(!_vs_shader_methods[ShaderPhase]) _vs_shader_methods[ShaderPhase]=[];
			shaderName[ShaderPhase].forEach(function(e){  _vs_shader_methods[ShaderPhase].push(e);  });
		}
		var shaderName = node.fragment_ShaderName;
		for (var ShaderPhase in shaderName) {
			if(!_fs_shader_methods[ShaderPhase]) _fs_shader_methods[ShaderPhase]=[];
			shaderName[ShaderPhase].forEach(function(e){  _fs_shader_methods[ShaderPhase].push(e);  });
		}
	}
	if(window.egret3d){
		if(!_vs_shader_methods[egret3d.ShaderPhaseType.start_vertex]) _vs_shader_methods[egret3d.ShaderPhaseType.start_vertex]=[]
		_vs_shader_methods[egret3d.ShaderPhaseType.start_vertex].push("particle_vs");
	}
	return { _vs_shader_methods:_vs_shader_methods, _fs_shader_methods: _fs_shader_methods };
}


function phaseEnd (_passUsage, shader_methods) {
	var _vs_shader_methods=shader_methods._vs_shader_methods;
	var _fs_shader_methods=shader_methods._fs_shader_methods;
	_passUsage.vertexShader = [];
	_passUsage.fragmentShader = [];
	
    var shaderList;
    shaderList = _vs_shader_methods[egret3d.ShaderPhaseType.utils_vertex];
    if (shaderList && shaderList.length > 0)
        addMethodShaders(_passUsage.vertexShader, shaderList);
    shaderList = _vs_shader_methods[egret3d.ShaderPhaseType.base_vertex];
    if (shaderList && shaderList.length > 0) {
        addMethodShaders(_passUsage.vertexShader, shaderList)
    } else {
        addMethodShaders(_passUsage.vertexShader, ["base_vs"]);
        shaderList = _vs_shader_methods[egret3d.ShaderPhaseType.start_vertex];
        if (shaderList && shaderList.length > 0)
            addMethodShaders(_passUsage.vertexShader, shaderList);
        else
            addMethodShaders(_passUsage.vertexShader, ["diffuse_vertex"]);
        shaderList = _vs_shader_methods[egret3d.ShaderPhaseType.local_vertex];
        if (shaderList && shaderList.length > 0)
            addMethodShaders(_passUsage.vertexShader, shaderList);
        shaderList = _vs_shader_methods[egret3d.ShaderPhaseType.global_vertex];
        if (shaderList && shaderList.length > 0)
            addMethodShaders(_passUsage.vertexShader, shaderList);
        shaderList = _vs_shader_methods[egret3d.ShaderPhaseType.end_vertex];
        if (shaderList && shaderList.length > 0)
            addMethodShaders(_passUsage.vertexShader, shaderList);
        else
            addMethodShaders(_passUsage.vertexShader, ["end_vs"]);
        addMethodShaders(_passUsage.vertexShader, ["out_vs"])
    }
    shaderList = _fs_shader_methods[egret3d.ShaderPhaseType.utils_fragment];
    if (shaderList && shaderList.length > 0)
        addMethodShaders(_passUsage.fragmentShader, shaderList);
    shaderList = _fs_shader_methods[egret3d.ShaderPhaseType.base_fragment];
    if (shaderList && shaderList.length > 0) {
        addMethodShaders(_passUsage.fragmentShader, shaderList)
    } else {
        addMethodShaders(_passUsage.fragmentShader, ["base_fs"]);
        shaderList = _fs_shader_methods[egret3d.ShaderPhaseType.start_fragment];
        if (shaderList && shaderList.length > 0)
            addMethodShaders(_passUsage.fragmentShader, shaderList);
        shaderList = _fs_shader_methods[egret3d.ShaderPhaseType.materialsource_fragment];
        if (shaderList && shaderList.length > 0)
            addMethodShaders(_passUsage.fragmentShader, shaderList);
        else
            addMethodShaders(_passUsage.fragmentShader, ["materialSource_fs"]);
        shaderList = _fs_shader_methods[egret3d.ShaderPhaseType.diffuse_fragment];
        if (shaderList && shaderList.length > 0)
            addMethodShaders(_passUsage.fragmentShader, shaderList);
        else
            addMethodShaders(_passUsage.fragmentShader, ["diffuse_fragment"]);
        shaderList = _fs_shader_methods[egret3d.ShaderPhaseType.normal_fragment];
        if (shaderList && shaderList.length > 0)
            addMethodShaders(_passUsage.fragmentShader, shaderList);
        shaderList = _fs_shader_methods[egret3d.ShaderPhaseType.shadow_fragment];
        if (shaderList && shaderList.length > 0)
            addMethodShaders(_passUsage.fragmentShader, shaderList);
        shaderList = _fs_shader_methods[egret3d.ShaderPhaseType.specular_fragment];
        if (shaderList && shaderList.length > 0)
            addMethodShaders(_passUsage.fragmentShader, shaderList);
        shaderList = _fs_shader_methods[egret3d.ShaderPhaseType.lighting_fragment];
        if (shaderList && shaderList.length > 0)
            addMethodShaders(_passUsage.fragmentShader, shaderList);
        shaderList = _fs_shader_methods[egret3d.ShaderPhaseType.matCap_fragment];
        if (shaderList && shaderList.length > 0)
            addMethodShaders(_passUsage.fragmentShader, shaderList);
        shaderList = _fs_shader_methods[egret3d.ShaderPhaseType.end_fragment];
        if (shaderList && shaderList.length > 0)
            addMethodShaders(_passUsage.fragmentShader, shaderList);
        else {
            addMethodShaders(_passUsage.fragmentShader, ["end_fs"])
        }
        shaderList = _fs_shader_methods[egret3d.ShaderPhaseType.multi_end_fragment];
        if (shaderList && shaderList.length > 0)
            addMethodShaders(_passUsage.fragmentShader, shaderList);
        addMethodShaders(_passUsage.fragmentShader, ["out_fs"])
    }
    return _passUsage;
}
function addMethodShaders(passUsageShaders, shaderList){
	if(shaderList) shaderList.forEach(function(e){  passUsageShaders.push(e); });
}
function getMainFunc(src){
	var mainTag = 'void main(';
	var mainPos = src.indexOf(mainTag);
	if (mainPos=== -1) return {globals:src, main:'' };
	for (var ii= mainPos; ii< src.length; ii++){
		if (src[ii] === '{'){
			 break;
		}
	};
	var globals = src.substring(0,mainPos);
	var mainFunc = src.substring( ii + 1 , src.lastIndexOf('}'));
	console.log({ 
		 globals:globals, main:mainFunc 
	})
	 return  { 
		 globals:globals, main:mainFunc 
		};
}

function getDefines (src){
	var index =src.lastIndexOf('#define ');
	if (index === -1) return {src:src, defines:''};
	for (var ii= index; ii< src.length; ii++){
		if (src[ii] === '\n' || src[ii] === '\r'){
			break;
		}
	};
	var defines = src.substring(0,ii);
	return { defines:defines,  src: src.substring(ii) };
}
function build(shaderList, defines){
	shaderList = shaderList.map(function(e){
		var src =  typeof aaa ==='undefined' ? egret3d.ShaderLib.lib[e] : aaa[e];
		if (!src) return {};
		var defines_src = getDefines(src);
		var defines_globals_main = getMainFunc(defines_src.src);
		defines_globals_main.defines = defines_src.defines;
		return defines_globals_main;
	});
	
	var globals='';
	var main='';
	defines= defines || '';
	for (var shader of shaderList) {
		if (shader.main) main+= shader.main;
		if(shader.globals)globals+= shader.globals;
		if(shader.defines)defines+= shader.defines + '\n';
	}
	main  = 'void main() {\n' + main + '\n}';
	console.log(defines + '\n' + globals + '\n' + main + '\n');
}

})();
