# 情境一

> 你在目前的 branch 修改、新增了一些檔案，但在還沒告一段落前，臨時有更重要的任務須到其他 branch 去工作。

若直接切換分支，會出現以下警告且無法成功切換分支：

```plaintext
error: Your local changes to the following files would be overwritten by checkout:
.
.
.
Please commit your changes or stash them before you switch branches.
Aborting
```

此時有兩種做法：

- 先 add + commit，然後到其他 branch 處理其它任務，完成其它任務後再回來原 branch 恢復上一動 (`git reset HEAD^ --hard`)
- 若不希望仍然一團糟的程式碼進入 commit history，可以改用 `git stash`（詳見後續）

### Step1: 將進行到一半的工作暫存

```bash
git stash push -u
```

執行此指令後，directory 會回到最後一次 commit 時的狀態（也就是你進行到一半的 unstaged changes 會暫時全部消失）。

若 unstaged changes 中不包含 Untracked files（也就是沒有新增任何檔案），則不須使用 `-u` option。

### Step2: 放心地到其他分支執行重要任務

```bash
git checkout <ANOTHER-BRANCH>

# After completeing the urgent task...
git add .
git commit -m "Your message"
```

### Step3: 回到原分支將之前暫存的狀態拿回來

```bash
git checkout <ORIGINAL-BRANCH>
git stash pop
```

# 情境二

> 你在目前的 branch 修改、新增了一些檔案，本來以為只是一個小改動所以沒有另開 branch，但改到後來發現事情有點大條，還是另開 branch 比較好，此時要如何將目前的 unstaged changes 搬移到新 branch，並將目前的 branch 恢復到改動前的狀態呢？

### Step1: 將進行到一半的工作暫存

```bash
git stash push -u
```

### Step2: 新增並切換到新分支

```bash
git checkout -b <NEW-BRANCH>
```

此時新 branch 會和原 branch 一樣都在最後一次 commit 時的狀態（也就是不包含任何你進行到一半的 unstaged changes）。

### Step3: 將剛剛暫存的狀態套用在新分支上

```bash
git stash pop
```

> Stash 是所有 branches 共享的，也就是說「在 A branch 做的 stash，B branch 也可以拿來用」。

# 其他常用指令

### 列出所有 Stashes

```bash
git stash list
```

### 清空所有 Stashes

```bash
git stash clear
```

# 參考資料

- <https://git-scm.com/docs/git-stash>
- <https://gitbook.tw/chapters/faq/stash>