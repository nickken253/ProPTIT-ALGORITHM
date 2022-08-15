# WEEK 8: DYNAMIC PROGRAMING
*Câu hỏi kì này:*
- *`Quy hoạch động` là gì? Trạng thái là gì? Có những loại quy hoạch động nào? Khi nào cần sử dụng quy hoạch động?*
- *Nêu những bước cơ bản cần để giải quyết một bài toán quy hoạch động.*
- *Trình bày về 2 bài toán quy hoạch động kinh điển: Dãy con tăng dài nhất và Bài toán cái túi.*

## **I.TÌM HIỂU KHÁI QUÁT VỀ QUY HOẠCH ĐỘNG**
### **1. Khái niệm**
- `Quy hoạch động` là một phương pháp giải quyết các bài toán có tính chất gối nhau, được sử dụng khi có một công thức truy hồi.
> `Quy hoạch động` = Truy hồi + Ghi nhớ

- Bài toán sử dụng `Quy hoạch động` là bài toán có thể chia làm các bài toán con nhỏ hơn, rồi sẽ được chia làm các bài toán con nhỏ hơn nữa cho đến khi đủ đơn giản để tìm luôn được lời giải. Kết quả các bài toán sẽ được lưu lại để những lần tính toán tiếp theo nếu cần.
- Mỗi bài toán con ở đây còn được gọi là Trạng thái. Trạng thái là một trường hợp, một bài toán con của bài toán lớn.
- Nói cách khác, Đệ quy có nhớ chính là một dạng của `Quy hoạch động`.
### **2. Phân loại**
#### a. **`Top-down`** (Từ trên xuống):
- Khi giải quyết bài toán, chúng sẽ được chia làm các bài toán con, các bài toán này được giải quyết và ghi nhớ lời giải để dùng lại. Các bài toán này tiếp tục gọi ra bài toán con của chúng đến khi đủ dữ kiện để đưa ra kết quả tính toán.
- Đây chính là sử dụng Đệ quy có nhớ.
> Vd: Bài toán tính số Fibonacci thứ n.
``` C++
int F[big] = {};
int fibo(int n)
{
    if(n == 0 || n == 1) return 1;
    if(F[n] != 0) return F[n]; // Nếu F[n] đã được lưu trữ thì gọi lại kết quả, không cần phải tính lại.
    else F[n] = fibo(n - 1) + fibo(n - 2);
    return F[n];
}
```
> Vì kết quả tính ra được lưu lại để sử dụng, nên độ phức tạp của thuật toán được giảm đi đáng kể, không phải đi sâu. Với số thứ n, ta chỉ cần tối đa n + 1 lần lưu trữ.
>> Độ phức tạp: $O(n)$
#### b. **`Bottom-up`** (Từ dưới lên):
- Đây là phương pháp `Quy hoạch động` khử đệ quy.
- Các bài toán con đã có lời giải từ trước, ta chỉ cần dùng nó để xây dựng lên các bài toán phức tạp hơn.
> Vd: Bài toán tính số Fibonacci thứ n.
``` C++
int F[big];
int fibo(int n)
{
    F[0] = F[1] = 1;
    for(int i = 2; i <= n; i++)
    {
        F[i] = F[i - 1] + F[i - 2];
    }
    return F[n];
}
```
> Cách làm này tốt hơn **`Top-down`** về không gian bộ nhớ cho lời gọi hàm. Tuy nhiên, phương pháp này không trực quan bằng **`Top-down`** và mất công hơn để sắp xếp đúng thứ tự từ nhỏ tới lớn. >
>Nếu được sắp xếp đúng, cách này sẽ tốt hơn cài đặt **`Top-down`**.
>> Độ phức tạp: $O(n)$
### **3. Nhận xét**
- `Quy hoạch động` là kỹ thuật, không phải một thuật toán cụ thể nào cả, dùng để cải thiện hai nhược điểm của Đệ quy: sử dụng bộ nhớ lớn, Thời gian tính toán lâu.
- `Quy hoạch động` là một phương pháp khó, mỗi bài toán đều cần một cách tối ưu riêng, nên cần nằm vững bản chất của `Quy hoạch động`.
> Ta sử dụng `Quy hoạch động` khi:
> - Tìm được Hệ thức truy hồi. Tức là bài toán lớn được giải quyết dựa vào các bài toán con lồng nhau.
> - Một hoặc một vài bài toán con đã biết kết quả, sau đó giải quyết các bài toán lớn hơn.
- **Ưu điểm:** Tối ưu, thời gian chạy nhanh.
- **Nhược điểm:**
  - Tìm công thức truy hồi khó, chốt các bài toán con không hề đơn giản, các bài toán con có thể không gộp lại được bài toán lớn.
  - Số lượng bài toán con cần giải quyết lớn.

## **II. XÂY DỰNG BÀI TOÁN QUY HOẠCH ĐỘNG**
- Xác định bài toán: Một bước căn bản trong tất cả các bài toán, ta cần nắm rõ được đề bài và đề ra được cách sử dụng kiến thức cho phù hợp.
- Tìm bài toán cơ sở: Ta xây dựng bài toán tổng quát nhất cho tất cả các trường hợp xảy ra. Một số trường hợp ta tìm các bài toán con cơ sở.
- Xây dựng công thức truy hồi.
- Thực hiện truy vết: Khi tìm phương pháp tối ưu nhất, ta phải lưu lại con đường tối ưu đó để có thể sử dụng lại trong các bài toán mở rộng.

> Nhận xét: 
> - `Quy hoạch động` trong mỗi bài toán là khác nhau, nếu đặt bài toán khác nhau thì cách giải quyết là khác nhau, nếu đặt sai bài toán hoặc chưa đủ sẽ dẫn đến công thức truy hồi sai.

## III. BÀI TẬP VÍ DỤ
### 1. Dãy con tăng dài nhất
Link bài: [DÃY CON TĂNG DÀI NHẤT - LIQ](https://vn.spoj.com/problems/LIQ)
> **CODE MẪU:**
``` C++
int main()
{
    ios_base::sync_with_stdio(false);cin.tie(0);cout.tie(0);
    int n;
    cin >> n;
    int a[n + 10];
    int f[n + 10] = {};
    for(int i = 1; i <= n; i++)
    {
        cin >> a[i];
    } 
    a[0] = f[0] = 0;
    for(int i = 0; i <= n; i++)
    {
        f[i] = 1;
        for(int j = i - 1; j >= 1; j--)
        {
            if(a[j] < a[i])
            {
                f[i] = max(f[j] + 1, f[i]);
            }
        }
    }
    int maxx = 1;
    for(int i = 1; i <= n; i++)
    {
        if(f[i] >= maxx) maxx = f[i];
    }
    cout << maxx << endl;
```

### 2. Bài toán Cái túi
Link bài: [CÁI TÚI - SPOJ](https://www.spoj.com/PTIT/problems/BCCAITUI/)
> **CODE MẪU**
