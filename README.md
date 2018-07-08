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
	for(int k=1;k< number;k++){
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
	for(int i=0;i< number;i++){
        array[i]=rand()%100;       //亂數範圍限制在100以內 
        std::cout<<array[i]<<"  ";
	}
	cout<<"\n";
	cout<<"經過轉換後結果\n";</pre></code>
	
之後會在這裡放入主要演算法部分
==============================
        for(int i=0;i< number;i++){
        std::cout<<array[i]<<"  ";
	}
	check(array,number);
	return 0;
}</pre></code>

泡沫排序法
---------------
第一輪從array[1]檢查到array[number]<br/>
若發現其大小比他左邊的數還要小，則進行交換<br/>
第一輪交換結束後，陣列最右邊的數必為整個陣列的最大值，以後不必再檢查他<br/>
第二論從array[1]檢查到array[number-1]<br/>
以此類推....
<pre><code>int flag;  //用來顯示這一輪還有無需要交換的情形，如果沒有就可以結束bubble 
	for(int i=number-1;i>=1;i--){
		flag=0;     
		for(int j=1;j<=i;j++){
			if(array[j]< array[j-1]){  //若為true表示還有需要交換的情形
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
  -------------
  先從array[1]開始往他以左的所有元素比較大小<br/>
  如果比左邊的數小，就不斷地跟左邊的數交換直到他已經到最左邊了(array[0])<br/>
  然後再換array[2]不斷跟他的左邊元素做比較<br/>
  以此類推.....
  <pre><code>for(int i=1;i<number;i++){
		for(int j=i;j>=1;j--){
			if(array[j]< array[j-1]){
				int temp=array[j];
				array[j]=array[j-1];
				array[j-1]=temp;
			}
		}
	} </pre></code>
  
選擇排序法
---------------
不斷從所有陣列元素中找到最小的元素，然後放到最右邊<br/>
每輪交換結束時，最左邊的必定是所有元素中的最小值，故下一輪就不用再考慮他<br/>
<pre><code>int temp,change;        //temp為該輪中目前最小值，change為該目前最小值的index值 
	for(int i=0;i< number;i++){
		temp=array[i];
		for(int j=i;j< number;j++){		
			if (array[j]< temp){
				temp=array[j];
				change=j;
			}
		}
		array[change]=array[i];
		array[i]=temp;	
	}</pre></code>

快速排序法
-------------
函數宣告
<pre><code>void quicksort(int array[],int left,int right);</pre></code>
主程式呼叫
<pre><code>quicksort(array,0,number-1);</pre></code>
副函數
<pre><code>void quicksort(int array[],int left,int right){  //此處的left與right皆為陣列的index值 
	int compare=array[left];   //將陣列最左邊第一個元素指定給compare儲存 
	int i,j,temp1,temp2;
	i=left+1;   //從最左邊的下一個元素開始做判斷 
	j=right;
	if(left> right-1)    //如果現在left值=right值，甚至left已經在right右邊時，應該停止遞迴 
		return;
	if(left==right-1){     //如果現在陣列只剩下2個元素，則直接比較兩元素大小，順序相反則交換 
		if(array[left]> array[right]){
			temp1=array[left];
	    	array[left]=array[right];
	    	array[right]=temp1;
		}
	}
	else{     //left的右邊至少有2個元素(含)以上時，執行快速交換 
		while(i< j){    //索引值i與j若相撞則停止執行 
		for(;array[i]< compare&&i<=right;i++);    //索引i不斷往右，直到找到比compare大的元素 
		//此時array[i]的值比compare大，並且array[i]的左側元素皆會小於compare 
		//如果compare已經是陣列中最大的數，將會使索引 i=right+1 ， 表示從array[1]到array[right]的值小於compare 
	    for(;array[j]>=compare&&j> i;j--);    //索引j不斷往左，直到找到比compare小的元素，但不能比i還要左邊 
	    if(i<j){    //將索引i的元素與索引j的元素互換
		//不會執行此運算的情況有: 
		//1. i與j有碰到(若碰到就表示j已經無法從i的右邊找到比compare還要小的數了，則該結束了) 
		//2. i比j還要右邊(表示compare是陣列的最大值，使得i為right+1，那也該結束了) 
		    temp2=array[i];
	    	array[i]=array[j];
		    array[j]=temp2;
        	}
    	}
    	//此處會在i>=j時執行(也就是已經進行交換完) 
	    array[left]=array[i-1];    //把compare與索引i的前一個元素互換(因為array[i]的左側元素皆會小於compare) 
	    array[i-1]=compare;
	    //顯示即將傳入下一層遞迴的left、middle、right 
	    std::cout << left << " " << i-1 << " " << right << "\n";
	    //先檢視目前整個陣列的交換情形 
	    for(int k=0;k <=number-1;k++){
            std::cout << array[k] <<"  ";
	    }
	    std::cout <<"\n";
	    //再依序行左側與右側的遞迴 
     	quicksort(array,left,i-2);
	    quicksort(array,i,right);
	}
	std::cout << "\n";
}</pre></code>


合併排序法
------------
函數宣告
<pre><code>void segment(int array[],int temparray[],int left,int right);
void merge(int array[],int temparray[],int left,int middle,int right);</pre></code>
主程式呼叫
<pre><code>segment(array,temparray,0,number-1);</pre></code>
副函數segment部分
<pre><code>void segment(int array[],int temparray[],int left,int right){
	int middle;
	if(left<right){
		middle=(left+right)/2;
    	segment(array,temparray,left,middle);
    	segment(array,temparray,middle+1,right);
    	merge(array,temparray,left,middle,right);
    	for(int k=left;k<=right;k++)
    	    array[k]=temparray[k];
	}
} </pre></code>
副函數merge部分
<pre><code>void merge(int array[],int temparray[],int left,int middle,int right){
	int left_side=left;   //左半邊的牌從left開始 
	int right_side=middle+1;  //右半邊的牌從middle+1開始  
	int temparray_index=left;  //這裡要把左半邊的牌與右半邊的牌按照大小順序排列後，將值儲存在temparray[]
	//並且要儲存在temparray[]中的特定範圍，也就是索引值從left開始到right，所以此處temparray_index初始值為left
	while(left_side<=middle&&right_side<=right){
		//判斷左右兩副牌當中的第一個元素誰的值較小，較小者放入temparray[] 
		if(array[left_side]<=array[right_side]){  //必須要加上等號，如果兩組牌的第1張大小相同，將導致無法放入temparray[] 
			temparray[temparray_index]=array[left_side];
			left_side+=1;  //左邊這副牌的首牌換下一張(因為前一張已經放入temparray[]) 
			temparray_index+=1;   // temparray[]使用貯列方式儲存 
		}
		else{
			temparray[temparray_index]=array[right_side];
	    	right_side+=1;
	    	temparray_index+=1; 
		}
	}
	//接著處理剩下的牌，基本上下面的2個while迴圈只會執行其中一個(因為必定有其中一副牌已經全部放到temparray[]中 
	while(left_side<=middle)
		temparray[temparray_index++]=array[left_side++];
	while(right_side<=right)
		temparray[temparray_index++]=array[right_side++];
}</pre></code>
