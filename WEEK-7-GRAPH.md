# **WEEK 7 - GRAPH (ĐỒ THỊ)**
*Câu hỏi kì này:*

- *Khái niệm đồ thị cơ bản*
- *BFS và DFS*

Đồ thị là gì ?

Đơn đồ thị

Đa đồ thị

Đồ thị có hướng

Đồ thị vô hướng

## **I. TÌM HIỂU CHUNG VỀ ĐỒ THỊ**
### **1. Định nghĩa**
#### a. Đồ thị là gì ?
![Đồ thị](https://cdn.ucode.vn/uploads/2247/upload/qHIeSmCA.png)
>Đồ thị là một cấu trúc dữ liệu rời rạc, tập hợp các `đỉnh` *(nút)* và các `cạnh` *(cung)* nối giữa chúng.

> Kí hiệu: $G(V, E)$
- $V$ là số đỉnh
>Vd: (A, B, C, D)
- $E$ là số cạnh
>Vd: ({B, C}, {A, D}, {A}, {})

Mỗi một cạnh sẽ nối một cặp đỉnh. **`Số đỉnh`** đôi khi còn được gọi là **`số bậc`** của đồ thị

#### b. Đơn đồ thị *(Simple graph)* và Đa đồ thị *(Multigraph)*:
![Đơn - đa đồ thị](https://th.bing.com/th/id/R.0f84a9c2dd70583209bb8f4b147b9d2f?rik=gpETOpLy7zGqGA&riu=http%3a%2f%2fimage.slidesharecdn.com%2fvignan-130911102520-phpapp01%2f95%2fgraph-theory-10-638.jpg%3fcb%3d1378895377&ehk=D6hM0xINclTWSpEJacLglPOCArXRjbCz2F5iqHTqhLw%3d&risl=&pid=ImgRaw&r=0&sres=1&sresct=1)

- **Đơn đồ thị:** là đồ thị $G(V, E)$ có $V$ đỉnh, $E$ cạnh nối giữa **`hai đỉnh khác nhau`**.
- **Đa đồ thị:** là đồ thị có $V$ đỉnh, $E$ cạnh nối giữa hai đỉnh khác nhau , và giữa các đỉnh khác nhau có thể có **`nhiều hơn 1 cạnh nối`**, gọi là **"Cạnh bội"**.
- **Giả đồ thị:** là đồ thị có thêm các **`khuyên`** nối vào 1 đỉnh.

#### c. Đồ thị vô hướng *(Un-directed Graph)* và Đồ thị có hướng *(Directed Graph)*

![Đồ thị](https://courses.cs.ut.ee/2011/graphmining/uploads/Main/simple.png)

- Đồ thị vô hướng: Là đồ thị có các **`cạnh`** nối giữa hai đỉnh khác nhau không có thứ tự.
- Đồ thị có hướng: Là đồ thị có các **`cung`** nối giữa hai đỉnh khác nhau có thứ tự xác định. *(Hướng từ $A$ $\to$ $B$ khác hướng từ $B$ $\to$ $A$)*.
>Vd: Giống các cung đường một chiều, ...
- Đa đồ thị có hướng: Là đồ thị có các **`cung`** nối giữa hai đỉnh khác nhau có thứ tự xác định, cùng một chiều đi giữa 2 đỉnh có thể có nhiều hơn 1 cung nối, gọi là **"Cung lặp"**
>Lưu ý: Chỉ có giả đồ thị vô hướng.
### **2. Thuật ngữ trên đồ thị**
#### a. Cạnh liên thuộc.
- Một cạnh $X$ nối giữa 2 đỉnh $A$ và $B$ thì ta nói $X$ là cạnh liên thuộc của $A$ và $B$. Ngược lại, $A$ và $B$ là hai đỉnh đầu cạnh.
#### b. Khuyên.
- Một cạnh $X$ được gọi là khuyên khi 2 đầu của nó cùng được nối với 1 đỉnh.
#### c. Đỉnh kề.
- Hai đỉnh $A$ và $B$ gọi là kề, khi mà giữa chúng có một cạnh $X$ nối liền. Lúc đó, ta gọi $A$ là đỉnh kề của $B$, $B$ là đỉnh kề của $A$.

![Đồ thị](https://external-preview.redd.it/7uBn5pl2k36biBLJR5HS8eCzCUA_9aSU63sG4u2aBgE.jpg?auto=webp&s=c75dd2972fd4f8049b1b0756d6d9a9b563f42ecb)

#### d. Bậc.
- Bậc của đồ thị: Số các đỉnh của đồ thị.
>Vd: Đồ thị bậc 6 gồm 6 đỉnh $A, B, C, D, E, F$.
- Bậc của đỉnh: Số các cạnh liên thuộc của đỉnh đó.
>Vd: Đỉnh $E$ là đỉnh bậc 4 do có 4 cạnh liên thuộc.
## **II. BIỂU DIỄN TRÊN ĐỒ THỊ**
### **1. Ma trận kề**
![Ảnh](https://th.bing.com/th/id/R.be88c280b38d1693a6dadcaf92fc21b4?rik=dD%2fir%2bd%2fAoDhdQ&pid=ImgRaw&r=0)

Một ma trận kề (liền kề) là một mảng 2 chiều u $\times$ v, mỗi giá trị $a[i][j]$ đạt được là 1 hoặc 0. Nếu là $a[i][j] = 1$ thì chứng tỏ có một cạnh nối đỉnh i với đỉnh j.
- Ma trận kề có thể dùng cho cả đồ thị vô hướng và đồ thị có hướng. Tuy nhiên ở đồ thị có hướng, thì ma trận kề **`không`** phải ma trận đối xứng.
- **Ưu điểm:** Kiểm tra 2 đỉnh i, j có kề nhau hay không rất nhanh.
- **Nhược điểm:** luôn phải tốn $n^2$ bộ nhớ để lưu ma trận, mà không phụ thuộc vào số cạnh của đồ thị, bên cạnh đó, không thể biểu diễn được đồ thị có cạnh song song
 ### **2. Danh sách kề và Danh sách cạnh**
![Đồ thị](https://external-preview.redd.it/7uBn5pl2k36biBLJR5HS8eCzCUA_9aSU63sG4u2aBgE.jpg?auto=webp&s=c75dd2972fd4f8049b1b0756d6d9a9b563f42ecb)

- **Danh sách kề:** là danh sách liệt kê các đỉnh kề của đỉnh đang xét
> **Danh sách kề** có dạng sau:
>
> $A: B, D, E.$
>
> $B: A, C.$
>
> $C: B, E, F.$
>
> $D: A, E.$
>
> $E: A, C, D, F.$
>
> $F: C, E.$

- **Danh sách cạnh:** là danh sách liệt kê các cạnh của đồ thị, được biểu diễn bởi 2 đỉnh đầu cạnh.
> **Danh sách cạnh** có dạng sau:
> 
> $A, B.$
>
> $A, D.$
>
> $A, E.$
>
> $B, C.$
>
> $C, E.$
> 
> $...$

- Ưu điểm của **`Danh sách kề`**, **`Danh sách cạnh`**: Tiết kiệm được nhiều bộ nhớ hơn so với **`Ma trận kề`** khi không phải lưu trữ các cạnh không tồn tại. Tuy nhiên trường hợp xấu nhất vẫn có $n^2$ cạnh tồn tại.

## **III. CÁC THUẬT TOÁN TÌM KIẾM TRÊN ĐỒ THỊ**
### **1. Một số khái niệm liên quan**
- **`Đường đi`** có độ dài $n$ từ đỉnh $A$ đến $B$ trong đồ thị là dãy các đỉnh ($x_1$, $x_2$, $x_3$, $...$,  $x_n$) với $A =$ $x_1$, $B =$ $x_n$
- **`Đường đi`** có thể biểu diễn thành các dây cung: ($x_1$, $x_2$), ($x_2$, $x_3$), $...$, ($x_{n-1}$, $x_n$).
- Đỉnh A được gọi là đỉnh đầu, đỉnh B được gọi là đỉnh cuối của đường đi. Đường đi có `đỉnh đầu` trùng với `đỉnh cuối` ($A$ $\equiv$ $B$) được gọi là một **`chu trình`**.
- **`Đường đi`** hay **`Chu trình`** nếu không có hai cạnh nào được lặp lại, ta gọi là **`Đường đi đơn`** và **`Chu trình đơn`**.
### **2. Tìm kiếm theo chiều sâu _(Depth First Search - DFS)_**
![Ảnh](https://i.ytimg.com/vi/QzjmDGRLjMM/maxresdefault.jpg)
- DFS là thuật toán tìm kiếm theo chiều sâu trong đồ thị. Bắt đầu từ một đỉnh, ta tìm đến đỉnh con đầu tiên của nó, đến khi tới đỉnh không có đỉnh con, ta quay lui về đỉnh cha của nó và tìm các đỉnh con khác.
- Nói cách khác, DFS là cứ đi từ trên xuống dưới, nếu gặp ngõ cụt thì quay lại ngã rẽ gần nhất và đi tiếp. Tới khi nào đi hết tất cả các nhánh thì dừng.
- Ta có thể sử dụng giải thuật đệ quy quay lui để giải quyết DFS.
``` C++
vector<vector<int>> DanhSachKe(v);
int check[v];

int init()
{
    // KHỞI TẠO ĐỒ THỊ
    int v, e; // Graph có v đỉnh và e cạnh
    cin >> v >> e;
    for(int i = 0; i < v; i++) check[i] = 0;
        // check[i] = 0 là chưa duyệt
        // check[i] = 1 là đã duyệt
    for(int i = 0; i < e; i++)
    {
        int a, b; // a và b là 2 đỉnh kề nhau
        cin >> a >> b;
        DanhSachKe[a].push_back(b); // Cập nhật b vào danh sách kề của a
        DanhSachKe[b].push_back(a); // Cập nhật a vào danh sách kề của b
    }
}
```
>Đầu vào cần 1 đỉnh gốc $v$ và một mảng đánh dấu $check[N]$ các đỉnh để xem đỉnh đó đã được duyệt qua hay chưa.
>
> - Bước 1: Đánh dấu đỉnh $v$ đã được duyệt.
> - Bước 2: Lấy danh sách kề của $v$. Với mỗi đỉnh $i$ trong danh sách:
>   - Nếu $i$ chưa được duyệt thì chọn $i$ làm gốc mới và lặp lại các bước trên. 
``` C++
// DFS ĐỆ QUY
void DFS(int x)
{
    cout << x << " ";
    check[x] = 1; // Đánh dấu là đã duyệt qua đỉnh x
    for(int i = 0; i < DanhSachKe[x]. size(); i++) // Duyệt các đỉnh con của đỉnh x
    {
        int y = DanhSachKe[x][i]; // y là đỉnh con của x
        if(check[y] == 0)
        {
            DFS(y);
        }
    }
}
```
>**Example:**
>> **Input:**
>>
>> 7 6
>>
>> 1 2
>>
>> 1 3
>>
>> 2 4
>>
>> 2 5
>>
>> 3 6
>>
>> 3 7
>
>> **Output:**
>>
>> 1 2 4 5 3 6 7
- Bên cạnh đó, ta còn có thể sử dụng phương pháp `khử đệ quy`. Cách này phức tạp hơn vì ta phải dùng `Stack` để lưu các đỉnh chưa duyệt.
> Khởi đầu vẫn cần 1 đỉnh gốc $x$.
> - Bước 1: Thêm đỉnh gốc vào `Stack`.
> - Bước 2: Lặp lại khi `Stack` không rỗng
>   - Xét đỉnh $y$ ở đầu `Stack`.
>   - Nếu đỉnh $y$ đã được duyệt thì bỏ qua.
>   - Đánh dấu đã duyệt đỉnh $y$.
>   - Lấy danh sách đỉnh kề của $y$. Với mỗi đỉnh $i$, nếu $i$ chưa duyệt thì đẩy $i$ vào `Stack`.

``` C++
// DFS Stack
void DFS(int x)
{
    stack<int> st;
    st.push(x);
    while(st.size())
    {
        cout << st.top() << " ";
        int y = st.top();
        st.pop();
        if(check[y] == 1) continue;
        // Nếu không kiểm tra có thể xảy ra trường hợp đỉnh đã duyệt quay lại stack và duyệt lại nhiều lần.
        check[y] = 1;
        for(int i = 0; i < DanhSachKe[y]. size(); i++)
        {
            int tmp = DanhSachKe[y][i];
            if(check[tmp] == 0) st.push(tmp);
        }
    }
}
```
>**Example:**
>> **Input:**
>>
>> 7 6
>>
>> 1 2
>>
>> 1 3
>>
>> 2 4
>>
>> 2 5
>>
>> 3 6
>>
>> 3 7
>
>> **Output:**
>>
>> 1 3 7 6 2 5 4

*__`Lưu ý`__:* 
- *Kết quả của 2 phương pháp có thể khác nhau, do Stack hoạt động theo cơ chế LIFO, nên kết quả ở mỗi đỉnh sẽ bị in ngược lại. Tuy nhiên, nó vẫn tuân theo nguyên lý của DFS.*
- *Thuật toán sẽ duyệt qua tất cả các đỉnh nếu đồ thị liên thông. Tuy vậy, nó là thuật toán tìm kiếm mù, mang tính chất vét cạn và sẽ kém hiệu quả nếu tập đỉnh quá lớn.*
### **3.Tìm kiếm theo chiều rộng _(Breadth First Search - BFS)_**
- BFS hay Tìm kiếm theo chiều rộng là thuật toán tìm kiếm theo chiều rộng trong đồ thị. Bắt đầu từ đỉnh đang xét, ta sẽ duyệt trước tiên các đỉnh gần nó nhất, rồi mới duyệt các đỉnh xa hơn.
- Nói cách khác, nếu xếp đồ thị thành cây, thì BFS sẽ duyệt theo thứ tự các tầng từ cao xuống thấp, hết tầng trên mới xuống tầng dưới.
> Cách hiện thực thuật toán BFS cũng tương tự như DFS. Ta cần dùng 1 mảng $check[N]$ để kiểm tra đỉnh đã được duyệt hay chưa, và thay vì dùng Stack, ta sẽ dùng `Queue` để lưu đã đỉnh chưa duyệt đỉnh kề.
> - Bước 1: Đánh dấu đỉnh gốc $x$ đã duyệt.
> - Bước 2: Thêm $x$ vào `Queue` *(Vì chưa xét các đỉnh kề của $x$)*
> - Bước 3: Nếu vẫn còn đỉnh để xét:
>   - Lấy đỉnh $y$ từ Queue để xét các đỉnh kề của nó.
>   - Lần lượt duyệt các đỉnh kề của y. Với mỗi đỉnh $i$, thêm $i$ vào `Queue` để chuẩn bị cho việc xét các đỉnh kề của nó.
``` C++
// DFS STACK
void BFS(int x)
{
    queue<int> q;
    check[x] = 1;
    q.push(x);
    while(q.size())
    {
        cout << q.front() << " ";
        int y = q.front();
        q.pop();
        for(auto i : DanhSachKe[y])
        {
            if(check[i] == 0)
            {
                check[i] = 1;
                q.push(i);
            }
        }
    }
}
```
> **Thuật toán loang**
>> `Thuật toán loang` có tên gọi như vậy vì nguyên lý hoạt động của nó giống vết dầu loang. Từ một vết dầu nhỏ sẽ được loang ra xung quanh. `Thuật toán loang` trên ma trận cũng vậy, bạn sẽ duyệt một ô trên ma trận và sau đó duyệt các điểm xung quanh nó và dần loang ra để giải quyết bài toán.
>> 
>> Như trong trò chơi dò mìn, để giải quyết được trò chơi, bạn phải chọn một điểm ban đầu, và xử lí các thông tin tại đó để có thể dò được các bãi mìn xung quanh, và bạn sẽ làm như vậy đến khi không còn loang được nữa.
>>
>> Ngoài việc sử dụng BFS hay DFS để loang, bạn có thể loang chay bằng đệ quy, tuy nhiên thời gian sẽ không được tối ưu.
>
> Tham khảo bài [BÃI CỎ NGON NHẤT - SPOJ](https://www.spoj.com/PTIT/problems/BCGRASS/)

### 4. Độ phức tạp thuật toán.
> Độ phức tạp của BFS và DFS đều giống nhau, chỉ khác nhau ở cách dùng và biểu diễn đồ thị
>| Cách biểu diễn | Độ phức tạp         |
>|----------------|---------------------|
>| Ma trận        | $O($ $n^2$ $)$      |
>| Danh sách cạnh | $O(n$ $\times$ $m)$ |
>| Danh sách kề   | $O(max(n, m))$      |
## **IV. TÍNH LIÊN THÔNG CỦA ĐỒ THỊ**
### **1. Các định nghĩa liên quan**
#### a. Liên thông *(connected)*:
- Một đồ thị vô hướng gọi là `liên thông` nếu luôn tìm được đường đi giữa hai đỉnh bất kỳ của nó.
- Một đồ thị có hướng gọi:
  - **Liên thông mạnh**: Là đồ thị có hướng mà luôn tồn tại đường đi giữa mọi cặp điểm.
  - **Liên thông yếu**: Là đồ thị có hướng mà khi bỏ hướng thì đồ thị vô hướng tương đương đó `liên thông`.
#### b. Thành phần liên thông:
- Khi đồ thị $G(V, E)$ `không liên thông`, nhưng phân rã G ra thành một số `đồ thị con liên thông`, chúng đôi một **không** có đỉnh chung. Thì các đồ thị con đó được gọi là `Thành phần liên thông`.
- `Đồ thị liên thông` khi có số `Thành phần liên thông` là 1
#### c. Cầu - Trụ:
- Một cạnh được gọi là cầu, khi loại bỏ cạnh này, làm tăng số lượng Thành phần liên thông của đồ thị.
- Một đỉnh được gọi là trụ, khi loại bỏ trụ này và các cạnh liên thuộc, thì làm tăng số lượng Thành phần liên thông của đồ thị
![Đồ thị](https://vietcodes.github.io/img/cut-vertex.png)
> **Ví dụ**:
> - Cạnh $(9, 10)$ là một cầu.
> - Đỉnh $2$ là một trụ.

### 2. Đếm số Thành phần liên thông.
- Ta đơn giản là đếm số lần thực hiện lại DFS hoặc BFS là được.
``` C++
int main()
{
    int v, e; // Graph có v đỉnh và e cạnh
    cin >> v >> e;
    for(int i = 0; i < v; i++) check[i] = 0;
    for(int i = 0; i < e; i++)
    {
        int a, b;
        cin >> a >> b;
        DanhSachKe[a].push_back(b); 
        DanhSachKe[b].push_back(a); 
    }
    int cnt = 0;
    for(int i = 1; i <= v; i++)
    {
        if(check[i] == 0)
        {
            BFS(i);
            cnt++;
        }
    }
    cout << cnt;
}
```