# WEEK 6 - QUEUE 
*Câu hỏi kì này:*
- *Tìm hiểu cách hoạt động của QUEUE, DEQUE, PRIORITY QUEUE.*
- *Các thao tác trên của chúng.*
- *Độ phức tạp.*
## **I. QUEUE.**
### **1. Định nghĩa:**
**QUEUE** là một cấu trúc dữ liệu **container** dùng để lưu giữ các đối tượng theo cơ chế **FIFO** *(First In First Out)*.

QUEUE khác với STACK ở điểm: QUEUE là một ống có 2 đầu, vào 1 đầu và đi ra ở đầu còn lại. STACK thì là một chiếc thùng, vào, ra chung 1 đường.

![Minh họa QUEUE](https://www.fluentcpp.com/wp-content/uploads/2018/01/queue.png)
### **2. Thao tác:** 
#### a. Khai báo:
``` C++
// THƯ VIỆN
#include<queue>
// KHAI BÁO
queue<int> q;
```
#### b. Hàm sử lý:

- **empty()** Kiểm tra xem hàng đợi hiện tại có đang rỗng hay không.
- **size()** Trả về kích thước hàng đợi hiện tại.
- **front()** Trả về phần tử đầu tiên của hàng đợi.
- **back()** Trả về phần tử cuối cùng của hàng đợi.
- **push()** Nạp thêm một phần tử vào hàng đợi
- **pop()** Xóa một phần tử ở đầu của hàng đợi.
> Các hàm trên đều có độ phức tạp là **O(1)**.


``` C++

```
## **II. PRIORITY QUEUE**
### **1. Định nghĩa:**
**PRIORITY QUEUE** là một kiểu dữ liệu tập hợp đặc biệt, được xây dựng từ **QUEUE** nhưng trong đó mỗi phần tử có một độ ưu tiên nhất định.

Đối với **PRIORITY QUEUE**, phần tử vào trước chưa chắc đã ra trước, nó còn phụ thuộc vào độ ưu tiên của các phần tử trong hàng đợi:
- Một phần tử có độ ưu tiên cao sẽ được *dequeued* (xóa khỏi **PRIORITY QUEUE**) trước một phần tử có độ ưu tiên thấp.
- Nếu hai phần tử có cùng độ ưu tiên, lúc này việc phần tử nào được xử lý trước sẽ phụ thuộc vào thứ tự của chúng ở trong **PRIORITY QUEUE**.

### **2. Thao tác:** 
#### a. Khai báo:
> Dùng chung thư viện với **QUEUE**
``` C++
// THƯ VIỆN
#include<queue>
// KHAI BÁO
priority_queue <int> pq; 
```
Mặc định khi khai báo, **PRIORITY QUEUE** sẽ có phép toán nhỏ hơn *(Loại những phần tử lớn hơn ra ngoài queue)*. Ngoài ra còn có các phép toán khác: 
>**greater**: lớn hơn 
>
>**equal_to**: bằng 
>
>**not_equal_to**: không bằng 
>
>**greater_equal**: lớn hơn bằng
> 
>**less_equal**: nhỏ hơn bằng

VD:
``` C++
priority_queue <int, vector<int>, greater<int>> pq;
```
#### b. Hàm sử lý:
> Các hàm thì sử dụng giống **STACK**

- **empty()** Kiểm tra xem hàng đợi hiện tại có đang rỗng hay không.
- **size()** Trả về kích thước hàng đợi hiện tại.
- **top()** Trả về phần tử đầu tiên của hàng đợi.
- **push()** Nạp thêm một phần tử vào hàng đợi
- **pop()** Xóa một phần tử ở đầu của hàng đợi.
> Các hàm trên đều có độ phức tạp là **O(1)**, trừ hàm **q.push()** có độ phức tạp là **O(log(q.size()))**.

## **III. DEQUE**
### **1. Định nghĩa:**
- **DEQUE** là cấu trúc dữ liệu chứa 0 hoặc nhiều phần tử có cùng kiểu dữ liệu và được biểu diễn bằng một hàng có phần tử đầu *(front)* và phần tử cuối *(last)*. 
- **DEQUE** cho phép xử lý dữ liệu ở cả hai đầu của hàng đợi với độ phức tạp **O(1)**, điều này rất hữu ích trong các ứng dụng nhất định.

### **2. Thao tác:** 
- **push_front()** thêm vào đầu deque.
- **push_back()** thêm vào cuối deque.
- **pop_front()** xóa phần tử đầu khỏi deque.
- **pop_back()** xóa phần tử cuối khỏi deque.
- **front()** trả về giá trị đầu deque.
- **back()** trả về giá trị cuối deque.
- **size()** trả về số lượng phần tử hiện tại trong deque.
- **empty()** kiểm tra xem deque hiện tại có đang rỗng hay không.
- **clear()** xóa hết các phần tử của deque.
> Các hàm trên đều có độ phức tạp là **O(1)**.
## **IV. BÀI TẬP VẬN DỤNG**
### **1. BCQUEUE**
Link bài: [BCQUEUE - SPOJ](https://www.spoj.com/PTIT/problems/BCQUEUE/)

>Code mẫu:
``` C++
#include <bits/stdc++.h>
using namespace std;
#define endl "\n"
#define ll long long

int main() {
    int n, inp;
    cin >> n;
    queue<int> q;
    while(n--) 
    {
        int inp;
        cin >> inp;
        if (inp == 1) cout << q.size() << endl;
        else if (inp == 2) 
        {
            if (q.empty() == true) cout << "YES" << endl;
            else cout << "NO" << endl;
        } 
        else if (inp == 3) 
        {
            cin >> inp;
            q.push(inp);
        } 
        else if (inp == 4) 
        {
            if (q.size()) q.pop();
        } 
        else if (inp == 5) 
        {
            if (q.size()) cout << q.front() << endl;
            else cout << -1 << endl;
        } 
        else if (inp == 6) 
        {
            if (q.size()) cout << q.back() << endl;
            else cout << -1 << endl;
        }
    }
}
```
### **2. TRÒ CHƠI VỚI QUEUE**
Link bài: [TRÒ CHƠI VỚI QUEUE - SPOJ](https://www.spoj.com/PTIT/problems/P175SUME/)
> **Đề bài:**
>
> Do những ngày hè quá nóng bức và nhàm chán nên Tide đã nghĩ ra một trò chơi khá thú vị với queue. 
>
> Ban đầu trong queue có 5 số 1, 2, 3, 4, 5 với mỗi lượt chơi Tide sẽ xóa phần tử ở đầu queue và cho 2 phần tử đó xuống cuối của queue và cứ tiếp tục cho đến khi Tide cảm thấy mệt và không chơi được nữa.
>
> Ví dụ tại lượt chơi thứ nhất trạng thái của queue là 1, 2, 3 ,4 ,5
Tại lượt chơi thứ 2 trạng thái của queue là 2, 3, 4, 5, 1, 1
>
> Các bạn hãy giúp Tide xác định xem số đầu tiên của queue tại lượt chơi thứ N nhé.
