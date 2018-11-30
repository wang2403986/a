# a

if(j+3<= endIndex){
		if(path[i]>>0===path[i+2]>>0){
		  if(path[j+1]===path[j+3]){
	      if(path[i+1]<path[i+3]){
	        if(path[i+3]-path[i+1]>=1.5){
	          moveY = (path[j+1]>>0) -1+0.75;
	          moveX = path[j];
            path[j+1] = path[j+3];
            path[j] =(path[j]<path[j+2])? path[j]+1  :   path[j]-1;
            if(path[j]!==path[j+2]){
              this.pathCurrent -=2;
            }
          }
	      }else{
	        if(path[i+1]-path[i+3]>=1.5){
	          moveY = (path[j+1]>>0) +1+0.25;
            moveX = path[j];
            path[j+1] = path[j+3];
            path[j] =(path[j]<path[j+2])? path[j]+1  :   path[j]-1;
            if(path[j]!==path[j+2]){
              this.pathCurrent -=2;
            }
          }
	      }
	    }
		}else if(path[i+1]>>0===path[i+3]>>0){
		  if(path[j]===path[j+2]){
		    if(path[i]<path[i+2]){
          if(path[i+2]-path[i]>=1.5){
            moveX = (path[j]>>0) -1+0.75;
            moveY = path[j+1];
            path[j] = path[j+2];
            path[j+1] =(path[j+1]<path[j+3])? path[j+1]+1  :   path[j+1]-1;
            if(path[j+1]!==path[j+3]){
              this.pathCurrent -=2;
            }
          }
        }else{
          if(path[i]-path[i+2]>=1.5){
            moveX = (path[j]>>0) +1+0.25;
            moveY = path[j+1];
            path[j] = path[j+2];
            path[j+1] =(path[j+1]<path[j+3])? path[j+1]+1  :   path[j+1]-1;
            if(path[j+1]!==path[j+3]){
              this.pathCurrent -=2;
            }
          }
        }
	    }
		}
