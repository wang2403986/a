float determinant(mat2 m) {
  return m[0][0]*m[1][1] - m[1][0]*m[0][1] ;
}
float determinant(mat4 m) {
  mat2 a = mat2(m);
  mat2 b = mat2(m[2].xy,m[3].xy);
  mat2 c = mat2(m[0].zw,m[1].zw);
  mat2 d = mat2(m[2].zw,m[3].zw);
  float s = determinant(a);
  return s*determinant(d-(1.0/s)*c*mat2(a[1][1],-a[0][1],-a[1][0],a[0][0])*b);
}

mat4 matrix;
void decompose(mat4 te){
float sx = length(te[0].xyz);
float sy = length(te[1].xyz);
float sz = length(te[2].xyz);
float det = determinant(te);
	if ( det < 0.0 ) sx = - sx;
followTargetPosition = te[3].xyz;
matrix = te;
float invSX = 1.0 / sx;
float invSY = 1.0 / sy;
float invSZ = 1.0 / sz;
matrix[0].xyz *=invSX;
matrix[1].xyz *=invSY;
matrix[2].xyz *=invSZ;
followTargetScale = vec3(sx,sy,sz);
}


