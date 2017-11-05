# Finding-the-number-discontinuity-of-adjacent-lattices

Finding the number discontinuity of adjacent lattices

	把1-8这8个数放入下图8个格中,要求相邻的格(横,竖,对角线)上填的数不连续.
  
    ┌─┐
    │①│
    
┌─┼─┼─┐
│②│③│④│

├─┼─┼─┤
│⑤│⑥│⑦│

└─┼─┼─┘
    │⑧│
    
    └─┘
【参考程序】

const lin:array[1..8] of set of  1..8 =

	 ([3,2,4],[1,6,3,5],[5,7,1,2,4,6],[1,6,3,7],
   
	 [3,8,2,6],[2,4,3,5,7,8],[3,8,4,6],[5,7,6]);
   
var a:array[1..8] of integer;

    total,i:integer;	had:set of 1..8;
    
function ok(dep,i:integer):boolean; {判断是否能在第dep格放数字i}

var j:integer;

begin

     ok:=true;
     
     for j:=1 to 8 do	 {相邻且连续则不行}
     
	 if (j in lin[dep]) and (abs(i-a[j])=1) then ok:=false;
   
     if i in had then ok:=false; {已用过的也不行}
     
end;


procedure output;    {输出一种方案}

 var j:integer;
 
 begin
 
	  inc(total);	 write(total,':');
    
	  for j:=1 to 8 do write(a[j]:2);writeln;
    
end;

procedure find(dep:byte);

var i:byte;

begin

	   for i:=1 to 8 do   begin  {每一格可能放1-8这8个数字中的一个}
     
		if ok(dep,i) then begin
    
		   a[dep]:=i;  {把i放入格中}
       
		   had:=had+[i];  {设置已放过标志}
       
		   if (dep=8) then output
       
			       else find(dep+1);
             
             
		    a[dep]:=10;   {回溯,恢复原状态}
        
		    had:=had-[i];
        
		end;
    
	   end;
     
end;

begin

     fillchar(a,sizeof(a),10);
     total:=0; had:=[];
     find(1);
     writeln('End.');
end.
