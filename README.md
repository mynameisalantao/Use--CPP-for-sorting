排序法
===============
首先匯入標頭檔，接著定義變數
<pre><code>const int number=10; 
int array[number];</pre></code>  
number為所要的陣列長度 
<pre><code>void check(int array[],int number);</pre></code>  
宣告函數check用來檢查經過sorting後的陣列是否有按照大小順序排列，以下為函數定義

<pre><code>void check(int array[],int number){
	int error=0;
	for(int k=1;k<  number;k++){
		if(array[k]< array[k-1])
		error=1;
	}
	std::cout<<"\n";
	if(error==1)
	std::cout<<"There have some error!!";
	else
	std::cout<<"That's correct!!";
}</pre></code>

預設變數error=0<br/>
若檢查出在後面的元素小於在前面的元素，表示排序有問題<br/>
主程式部分:
<pre><code>int main(){
	using std::cout;
	srand(time(NULL));
	cout<<"Current random array:\n";
	for(int i=0;i<number;i++){
        array[i]=rand()%100;       //亂數範圍限制在100以內 
        std::cout<<array[i]<<"  ";
	}
	cout<<"\n";
	cout<<"經過轉換後結果:\n";</pre></code>

        for(int i=0;i<number;i++){
        std::cout<<array[i]<<"  ";
	}
	check(array,number);
	return 0;
}</pre></code>

泡沫排序法

<pre><code>int flag;  //用來顯示這一輪還有無需要交換的情形，如果沒有就可以結束bubble 
	for(int i=number-1;i>=1;i--){
		flag=0;     
		for(int j=1;j<=i;j++){
			if(array[j]<array[j-1]){  //若為true表示還有需要交換的情形
			    flag=1; 
				int temp=array[j];
				array[j]=array[j-1];
				array[j-1]=temp;
			}
		}
		if(flag==0)   //這一輪都沒有進行交換，可以不用再下一輪了 
		    break;
	}</pre></code>
  
  插入排序法
  <pre><code>for(int i=1;i<number;i++){
		for(int j=i;j>=1;j--){
			if(array[j]<array[j-1]){
				int temp=array[j];
				array[j]=array[j-1];
				array[j-1]=temp;
			}
		}
	} </pre></code>
  
  選擇排序法

  <pre><code>int temp,change;        //temp為該輪中目前最小值，change為該目前最小值的index值 
	for(int i=0;i<number;i++){
		temp=array[i];
		for(int j=i;j<number;j++){		
			if (array[j]<temp){
				temp=array[j];
				change=j;
			}
		}
		array[change]=array[i];
		array[i]=temp;	
	}</pre></code>


