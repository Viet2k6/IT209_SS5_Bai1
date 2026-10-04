# Bài 1: Khôi phục commit đã mất bằng Git Reflog

## 1. Mục tiêu

Thực hành sử dụng `git reflog` để tìm và khôi phục một commit đã bị mất khỏi lịch sử sau khi thực hiện `git reset --hard`.

## 2. Tạo commit

Tạo file `feature.txt`:

```bash
echo "Day la tinh nang quan trong" > feature.txt
```

Commit lần đầu:

```bash
git add .
git commit -m "Them tinh nang quan trong"
```

Sau đó bổ sung nội dung và tạo commit thứ hai:

```bash
echo "Noi dung bo sung" >> feature.txt
git add feature.txt
git commit -m "Bo sung tinh nang"
```

## 3. Giả lập mất commit

Thực hiện:

```bash
git reset --hard HEAD~1
```

Sau khi reset, commit `Bo sung tinh nang` không còn xuất hiện trong `git log`.

## 4. Tìm commit bằng Reflog

Sử dụng:

```bash
git reflog
```

Kết quả tìm được:

```text
6724510 HEAD@{1}: commit: Bo sung tinh nang
```

Hash của commit cần khôi phục là `6724510`.

## 5. Khôi phục commit

Sử dụng hash tìm được từ Reflog:

```bash
git reset --hard 6724510
```

Kiểm tra:

```bash
git log --oneline
```

Kết quả:

```text
6724510 (HEAD -> master) Bo sung tinh nang
a875bcd Them tinh nang quan trong
```

Kiểm tra nội dung:

```bash
cat feature.txt
```

Kết quả:

```text
Day la tinh nang quan trong
Noi dung bo sung
```

## 6. Kết quả

Commit `Bo sung tinh nang` đã được khôi phục thành công bằng `git reflog` và `git reset --hard`. Nội dung file cũng được khôi phục đầy đủ mà không cần viết lại thủ công.
