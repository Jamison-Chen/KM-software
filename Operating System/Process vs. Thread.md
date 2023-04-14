### Process (程序)

Process 是正在執行並且載入 RAM 的 Program，「執行應用程式」這個動作就是將 Program 活化成 Process。

-   Process 是電腦中正在執行的 Program
-   每一個 Process 是互相獨立的（不共享 CPU、RAM 等資源）
-   多個 Processes 間的溝通，只能透過由 OS 提供的 inter-process commuication
-   在 Multitasking Operating System 中，可以同時執行數個 Process，然而即使搭載這樣的 OS，一個 CPU 一次也只能執行一個 Process（因此才出現現在的多核處理器）
-   Process 會佔用 RAM，因此如何排程 (Scheduling)，以及如何有效管理記憶體是 OS 設計者須關注的事

### Thread (執行緒)

一個 Process 由多個 Threads 組成，每一個 Thread 負責某一項功能。以聊天室 Process 為例，可以同時接受對方傳來的訊息以及發送自己的訊息給對方，就是同個 Process 中不同 Threads 的功勞。

![[Process and thread.jpg]]

-   同一個 Process 底下的 Threads 共享資源，如 RAM、變數等，不同的 Processes 間則否
-   進行 **Threading** 時，多個 Threads 若同時存取同一個全域變數，可能導致 **Synchronization Problem**；若 Threads 間互搶資源，則可能產生 **Deadlock**，如何避免或預防上述兩種情況的發生也是 OS 所關注並改善的