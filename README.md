# 主要功能

輸入:

```
image_001.png
```

輸出:

```
<img src="/image/image_001.png" alt="image_001.png" />
```



# 安裝複製剪貼布功能

```bash
pip install pyperclip
```



# Source Code

```python


import threading
import tkinter as tk
import pyperclip as pc

def Window_on_Close():
    global win
    print("Windows close")
    win.destroy()

def btn_click():
    global Input
    global Text_1

    value = Input.get()
    str = "<img src=\"/image/" + value + ".png" + "\" " + "alt=\""  +  value +  ".png" + "\" />"

    Text_1.delete("0.0",tk.END)
    Text_1.insert(tk.END, str)
    Input.focus()
    pc.copy(str)
    print(str)


def Create_Win():
    global win
    win = tk.Tk()
    win.title("MD格式<img> 轉換")
    win.geometry("400x250")
    #==========  UI code here ====================

    global Input
    global Text_1

    label = tk.Label(win,text="請輸入檔名")
    label.pack()

    Input = tk.Entry(win)
    Input.pack(pady=10)

    btn = tk.Button(win,text="轉換並複製到剪貼簿",command=btn_click)
    btn.pack(pady=10,padx=10,ipadx=20)

    Text_1 = tk.Text(win)
    Text_1.pack(pady=10,padx=10)

    #=========================================
    win.protocol("WM_DELETE_WINDOW", Window_on_Close)
    win.mainloop()
    


if __name__ == "__main__":
    # 建立 TK UI Window 視窗
    task_1 = threading.Thread(target = Create_Win)
   
    task_1.start()

```

