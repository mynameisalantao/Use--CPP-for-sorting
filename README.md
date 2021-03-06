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

泡沫排序法(20180708)
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
  
  插入排序法(20180708)
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
  
選擇排序法(20180708)
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

快速排序法(20180708)
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


合併排序法(20180709)
------------
函數宣告
<pre><code>void segment(int array[],int temparray[],int left,int right);
void merge(int array[],int temparray[],int left,int middle,int right);</pre></code>
主程式呼叫
<pre><code>segment(array,temparray,0,number-1);</pre></code>
副函數segment部分
<pre><code>void segment(int array[],int temparray[],int left,int right){
	int middle;
	if(left < right){
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

堆積排序法(20180710)
----------
先將亂數陣列(array)排成最大堆(陣列queues) <br/>
接著再將最大堆的第一個元素(最大者)依序放入陣列result當中 <br/>
然後把queues的最後一個元素放到第一個位置重新進行最大堆排列的修正 <br/>
繼續重複把最大堆的第一個元素放入陣列result當中 <br/>
函數宣告
<pre><code>void add(int element);
void take(void);</pre></code>
主程式呼叫
<pre><code>for(int i=0;i < number;i++){
        array[i]=rand()%100;       //亂數範圍限制在100以內 
        cout << array[i] << "  ";
    }
    cout << "\n";
    //放入最大堆 
    for(int k=0;k < number;k++){  //依次將亂數產生出來的陣列輸入最大堆積當中 
    	add(array[k]);
	}
	cout << "\n";
	//想要印出樹狀結構 
	//每當x到達1,2,4,8...時就要換行，所以利用y不斷以2的倍數成長，當x=y時就換行 
	int y=1;   
	for(int x=1,z=1;z<=number;x++,z++){
		cout << queues[z-1] << " ";
		if(x==y){
			cout << "\n";
		    y*=2;
		    x=0;
	    }
		else
	        y=y;
	}
	cout << "\n";
	//從最大堆做大小排序 
	take();
	//印出最後結果 
	for(int k=0;k < number;k++){
		cout << result[k] << " ";
	}</pre></code>

副函數<br/>
放入最大堆函數
<pre><code>void add(int element){
	static int top=0;  //紀錄目前堆疊貯列最上方的指標(為queues陣列的索引值) 
	int point;  //紀錄目前新插入的元素所擺放的索引值 
	if(top==0){  //若目前堆疊是空的，就放在第一個 
		queues[0]=element;
		top++;
	}
	else{
		point=top;
		queues[top++]=element;
		while(point > 0){  //不斷與其父節點進行大小比較，若比父節點大則進行交換，直到變成第一個節點則停止執行
		    if(element > queues[(point-1)/2]){
		    	queues[point]=queues[(point-1)/2];
		    	queues[(point-1)/2]=element;
		    	point=(point-1)/2;  //將原本的index值與原本他的父節點index值進行交換 
			} 
			else  //如果比他的父節點還小，那就不用進行交換 
			break;
		}	
	}
	std::cout << "Current top" << " " << top << "\n";
	for(int i=0;i<=top-1;i++){
		std::cout << queues[i] << " ";
	}
	std::cout<<"\n";
}</pre></code>
從最大堆做大小排序函數
<pre><code>void take(){
	int queues_top=number;  //陣列 queues的頂 (指在貯列最後一個元素的後面)
	//int queues_front=0;  //陣列 queues的底(指在目前貯列的第一個元素上) 
	int result_top=0;  //陣列 result的top
	int temp;
	int point;  //在修正最大堆積時作為暫存使用 
	int bigger;
	while(0<=queues_top){
		result[result_top]=queues[0];  //將陣列queues的第一個元素放入resule陣列的最後面 
		//
		std::cout << "result_top=" << result_top << "  " << "result[result_top]=" << result[result_top] << " ";
		//
		result_top++;
		queues[0]=queues[queues_top-1];  //將原本貯列的最後一個元素填補最前面的空缺 
		//
		std::cout << "queues[0]=" << queues[0] << "\n";
		//
		queues_top--;
		point=0;
		while(2*point+1 < queues_top){  //若point的左子節點存在 
			if(2*point+2 < queues_top){  // 若point的右子節點也存在 
				bigger=queues[2*point+2] > queues[2*point+1]? 2*point+2:2*point+1;  //比較左右子節點誰比較大 
				if(queues[point] < queues[bigger]){  //若point節點比"左右子節點中較大者"還要小，則進行交換 
			    	temp=queues[point];
			    	queues[point]=queues[bigger];
			    	queues[bigger]=temp;
			    	point=bigger;  //把point指向新的位置 
		    	} 
		    	else  //若point節點比"左右子節點中較大者"還要大，則目前推疊位置正確，不用交換，故跳出迴圈 
		    	break;
		    } 
			else{  //若 point的左子節點存在，但 point的右子節點不存在，則point只要跟他的左子節比較大小即可  
				if(queues[point] < queues[2*point+1]){  //若point比他的左子節還要小，則需交換 
			    	temp=queues[point];
			    	queues[point]=queues[2*point+1];
			    	queues[2*point+1]=temp;
			    	point=2*point+1;
		    	}
		    	else  //若point比他的左子節還要大，則不用交換 
		    	break;
			}	
		}	
	}	
}</pre></code>

基數排序法(20180710)
--------------
我這裡是使用LSD(Least Signififant Digit)，也就是從最小位數開始進行分配<br/>
因為我這裡的亂數值是0到100之間，所以總共只會有2位數<br/>
我建立一個10乘10的矩陣來存放經過分配後的結果(個位數與十位數共用)<br/>
先取出每個數值的個位數，然後放入矩陣中<br/>
陣列的每一列代表他的個位數數值，然後目前行沒有排序關係<br/>
接著從第一行到第十行依序取出，放到陣列當中<br/>
如此一來個位數已經按照大小順序了<br/>
接著再根據十位數大小來分配到矩陣當中<br/>
最後再依序將每列元素取出，則可得到按照大小順序排列的陣列
<pre><code>using std::cout;
	int matrix[10][10]={0};  //根據(個位數和十位數共用)位數做分配的矩陣 
    int digit_top[10]={0};  //存放在矩陣matrix中每個陣列的top指標 
    int digit;  //暫存要判斷分配的數值(儲存個位數或十位數) 
    int top;  //暫存從digit_top[]取出的top值 
	cout << "原始亂數隨機陣列array[]:\n";
	//產生亂數，同時依照個位數分配陣列 
	srand(time(NULL));
	for(int i=0;i < number;i++){
        array[i]=rand() % 100;       
        cout << array[i] << "  ";
        digit=array[i] % 10;  //此處digit為array[i]的個位數 
        top=digit_top[digit];  //找出在matrix[][]中第digit個陣列，他目前的top值為多少 
        matrix[digit][top]=array[i];  //將數值array[i]放入matrix[][]矩陣中，第digit個陣列的第top個 
        digit_top[digit]++;  //top指標換指向下一個位置 
    }
    cout << "\n";
    //印出目前個位數分配矩陣matrix[][]的狀況 
    cout << "經過個位數分配後的矩陣matrix[][]:\n";
    for(int k=0;k < number;k++){
    	for(int i=0;i < number;i++){
    		cout << matrix[k][i] << " ";
		}
		cout << "\n";
	}
	//監視陣列 digit_top[]狀況 
	cout << "目前的陣列digit_top[]:\n";
	for(int i=0;i < number;i++)
	   cout << digit_top[i] << " ";
	cout << "\n";
	
	//接著要按照列的順序取出matrix[][]中的元素
	int digit_array[number]={0};  //按照個位數大小排列的陣列digit_array[] 
	int digit_array_top=0;  //陣列digit_array[]的top指標 
	for(int k=0;k < number;k++){  //從第0列到第number列 
		for(int i=0;i < digit_top[k];i++){  //抽取每列的元素就到他們的top就好 
			digit_array[digit_array_top]=matrix[k][i];
			digit_array_top++;
		}
    } 
    //按照個位數大小排列的陣列digit_array[]
    cout << "照個位數大小排列的陣列digit_array[]:\n";
    for(int i=0;i < number;i++){
    	cout << digit_array[i] << " ";
	}
	cout << "\n";
	//接著要清空matrix[10][10]與digit_top[10]，因為接著要改以十位數來做分配
	for(int i=0;i < 10;i++){
		for(int j=0;j < 10;j++)
			matrix[i][j]=0;
		digit_top[i]=0;
	}
	//照十位數分配陣列 
	for(int i=0;i < number;i++){       
        digit=digit_array[i]/10;  //此處digit為array[i]的十位數 
        top=digit_top[digit];  //找出在matrix[][]中第digit個陣列，他目前的top值為多少 
        matrix[digit][top]=digit_array[i];  //將數值digit_array[i]放入matrix[][]矩陣中，第digit個陣列的第top個 
        cout << "digit=" << digit << " " << "top=" << top << " " << "digit_array[i]=" << digit_array[i] << "\n";
        digit_top[digit]++;  //top指標換指向下一個位置 
    }
    cout << "\n";
    //印出目前十位數分配矩陣matrix[][]的狀況 
    cout << "經過十位數分配後的矩陣matrix[][]:\n";
    for(int k=0;k < number;k++){
    	for(int i=0;i < number;i++){
    		cout << matrix[k][i] << " ";
		}
		cout << "\n";
	}
	//因為已經全部取出digit_array[]中的數值，現在可以清掉了，方便等下放入最後的結果
	for(int i=0;i < number;i++)
        digit_array[i]=0;  //按照十位數大小排列的陣列digit_array[] 
	digit_array_top=0;  //陣列digit_array[]的top指標 
	//接著要按照列的順序取出matrix[][]中的元素
	for(int k=0;k < number;k++){  //從第0列到第number列 
		for(int i=0;i < digit_top[k];i++){  //抽取每列的元素就到他們的top就好 
			digit_array[digit_array_top]=matrix[k][i];
			digit_array_top++;
		}
    } 
    //按照十位數大小排列的陣列digit_array[](也就是依照大小順序排列)
    cout<< "照個十數大小排列的陣列digit_array[]:\n";
    for(int i=0;i < number;i++){
    	cout << digit_array[i] << " ";
	}
	cout << "\n";</pre></code>
