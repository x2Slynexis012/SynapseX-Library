# WinNap UI Library v3.1

Modern UI Framework for CustomTkinter Applications

WinNap คือไลบรารี UI สำหรับ Python (CustomTkinter) ที่ช่วยให้คุณสร้างแอปเดสก์ท็อปสไตล์ Modern ได้อย่างรวดเร็ว มีระบบหน้าต่าง, Sidebar Navigation, Page System, Card UI, Popup Dialog, Notification, Theme และคอมโพเนนต์พื้นฐานครบชุด

✅ **เวอร์ชัน 3.1:**

* ปรับปรุงระบบ Popup ให้เรนเดอร์สมบูรณ์
* เพิ่ม Input Dialog (text / password / number)
* ปรับ Notification Fade ให้ลื่นขึ้น

---

## คุณสมบัติหลัก (Features)

* Modern Borderless Window (ลากได้, topmost)
* Sidebar Navigation พร้อมระบบ Active Page
* Theme System (Dark, Light, Purple, Cyberpunk)
* Page System แบบอัตโนมัติ
* Card UI สำหรับจัดกลุ่มข้อมูล
* Popup Dialog (Alert / Confirm / Input)
* Notification แบบ Fade In / Fade Out
* ปุ่ม, สวิตช์, สไลเดอร์, ProgressBar, Entry, ComboBox
* Status Bar แสดงสถานะด้านล่าง
* รองรับ Callback ทุกระบบ

---

## Theme ที่มีให้

* dark
* light
* purple
* cyberpunk

เรียกใช้ด้วย

```python
WinNapTheme.get_theme("dark")
```

---

## การสร้างหน้าต่างหลัก

```python
app = WinNapWindow(
    title="My App",
    width=1000,
    height=700,
    theme="dark",
    topmost=True,
    resizable=True,
    center=True
)
```

---

## การสร้างหน้า (Page)

```python
home = app.add_page("home", "Dashboard", "🏠")
home.add_header("Dashboard", "หน้าหลักของระบบ")
```

✅ หน้าแรกจะถูกเปิดอัตโนมัติทันทีโดยไม่ต้องเรียก `switch_page()`

---

## คอมโพเนนต์ที่รองรับใน Page

```python
page.add_header(title, subtitle)
page.add_card(title)
page.add_section(title, description)
page.add_button(text, command)
page.add_switch(text, command)
page.add_label(text)
page.add_entry(placeholder)
page.add_slider(0, 100)
page.add_progressbar()
page.add_combobox(["Low", "Medium", "High"])
page.clear()
```

---

## การใช้งาน Card

```python
card = home.add_card("System Info")
card.add_label("Server: Online")
card.add_button("Restart", restart_func)
card.add_switch("Auto Mode", default=True)
```

---

## ระบบ Popup Dialog

### Alert

```python
app.show_alert("บันทึกข้อมูลสำเร็จ")
```

### Confirm

```python
app.show_confirm(
    "คุณต้องการลบหรือไม่?",
    on_confirm=confirm_func,
    on_cancel=cancel_func
)
```

### Input

```python
app.show_input(
    message="กรุณากรอกชื่อ",
    default_value="User",
    on_submit=submit_func,
    input_type="text"  # text / password / number
)
```

---

## ระบบ Notification

```python
app.show_notification("เชื่อมต่อสำเร็จ", 3)
```

---

## ระบบ Status Bar

```python
app.set_status("กำลังเชื่อมต่อเซิร์ฟเวอร์...")
```

---

## ตัวอย่างแอปแบบเต็ม (Example)

```python
app = WinNapWindow("WinNap Demo", 1100, 750, "cyberpunk")

home = app.add_page("home", "Dashboard", "🏠")
home.add_header("Dashboard", "หน้าหลักของระบบ")

card = home.add_card("System Status")
card.add_label("Server: Online")

home.add_button("แจ้งเตือน", lambda: app.show_notification("ยินดีต้อนรับ"))

settings = app.add_page("settings", "Settings", "⚙️")
settings.add_header("Settings")
settings.add_switch("Debug Mode")
settings.add_slider(0, 100)
settings.add_combobox(["Low", "Medium", "High"])

app.run()
```

---

## เหมาะสำหรับใช้งานกับ

* Control Panel
* Launcher
* Admin Panel
* Game Tool
* Cheat GUI
* Dashboard App

---

## เวอร์ชันปัจจุบัน

✅ **WinNap UI Library v3.1**

* Auto Start First Page
* Popup Input System
* Improved Notification System
* Popup Rendering Fix

---

## License

ใช้งานได้ฟรีทั้งเชิงพาณิชย์และส่วนตัว

---

## 💾 Popup Input + ระบบบันทึกข้อมูล (Save Data)

WinNap รองรับ Popup Input ที่สามารถนำค่าที่ผู้ใช้กรอกไปบันทึกลงไฟล์, ตัวแปร, หรือฐานข้อมูลได้โดยใช้ callback `on_submit`

---

### ✅ ตัวอย่างพื้นฐาน: บันทึกค่าลงไฟล์ `.txt`

```python
def save_name(value):
    with open("data.txt", "w", encoding="utf-8") as f:
        f.write(value)
    app.show_notification("บันทึกชื่อเรียบร้อย!")

home.add_button(
    "กรอกชื่อ",
    lambda: app.show_input(
        message="กรอกชื่อของคุณ",
        default_value="User",
        input_type="text",
        on_submit=save_name
    )
)
```

ผู้ใช้กรอกข้อมูล → กด OK → ระบบจะส่งค่ามาที่ `save_name(value)` และทำการบันทึกทันที

---

### ✅ ตัวอย่าง: บันทึกลงตัวแปรภายในโปรแกรม

```python
user_data = {"name": None}

def save_name(value):
    user_data["name"] = value
    app.show_notification(f"บันทึกชื่อแล้ว: {value}")

home.add_button(
    "ตั้งชื่อ",
    lambda: app.show_input(
        "กรุณากรอกชื่อ",
        on_submit=save_name
    )
)
```

เหมาะสำหรับเก็บค่าไปใช้งานภายในแอประหว่างรัน

---

### ✅ ตัวอย่าง: Popup Input แบบ Password + บันทึกลง JSON

```python
import json

def save_password(value):
    data = {"password": value}
    json.dump(data, open("user.json", "w"))
    app.show_notification("บันทึกรหัสผ่านสำเร็จ")

home.add_button(
    "ตั้งรหัสผ่าน",
    lambda: app.show_input(
        message="รหัสผ่านใหม่",
        input_type="password",
        on_submit=save_password
    )
)
```

---

### ✅ Input Types ที่รองรับใน Popup

| Type       | การใช้งาน      |
| ---------- | -------------- |
| `text`     | ข้อความทั่วไป  |
| `password` | ซ่อนรหัสผ่าน   |
| `number`   | ตัวเลขเท่านั้น |

---

### ✅ พฤติกรรมของ on_submit

* ทำงานเมื่อผู้ใช้กดปุ่ม OK
* ค่าที่กรอกจะถูกส่งเข้าฟังก์ชัน `on_submit(value)` ทันที
* สามารถนำไปบันทึกลงไฟล์, ฐานข้อมูล, API, หรือปรับ UI ต่อได้ทันที

---

หากต้องการเพิ่มระบบ:

* ✅ Save ลง Database (SQLite / MySQL)
* ✅ Save ขึ้น GitHub API
* ✅ Auto Load ข้อมูลตอนเปิดแอป
* ✅ Bind ค่า Popup กับ Label แบบ Real-time

สามารถต่อยอดจากระบบนี้ได้ทันที
