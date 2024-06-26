CAP Theorem 又叫做 Brewer's Theorem。

>一個服務最多只能同時確保 **consistency**、**availability** 與 **partition tolerance** 三者的其中兩個。
>
>\- Eric Brewer

![](<https://raw.githubusercontent.com/Jamison-Chen/KM-software/master/img/cap-theorem-2.png>)

### Consistency

Clients 總是可以從資料庫讀取到最新的資料。

### Availability

所有 Request 都會得到 non-error 的 response。

### Partition Tolerance

除了通訊問題以外，服務必須持續運作不間斷。

---

[ACID Model](</Database/ACID vs. BASE.md#ACID>) 的宗旨即「在具備 Partition Tolerance 的條件下，提供具備 Consistency 的服務」(CP)，銀行業通常會需要這種 Model。

相對地，[BASE Model](</Database/ACID vs. BASE.md#BASE>) 的宗旨為「在具備 Partition Tolerance 的條件下，提供具備 Availability 的服務」(AP)。

# 參考資料

- <https://en.wikipedia.org/wiki/CAP_theorem>
