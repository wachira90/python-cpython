# python-cpython
python-cpython

เร่งความเร็ว Python ด้วยแปลงไฟล์ .py เป็น .pyc และ .pyo

หากคุณต้องการเร่งความเร็ว Python ใน CPython คุณสามารถใช้วิธีแปลงไฟล์ .py เป็น .pyc และ .pyo ได้

ไฟล์ .pyc คือ ไฟล์ .py ที่ถูก CPython compile แปลงเป็น byte code แล้ว ช่วยให้สามารถนำได้เลยโดยไม่ต้องมา compile ใหม่

ไฟล์ .pyo คือ ไฟล์ .pyc ที่ถูกปรับแต่งประสิทธิภาพให้สามารถรันได้ดีขึ้นและมีประสิทธิภาพมากยิ่งขึ้น 

(ปัจจุบัน CPython ยกเลิกการสร้างเป็นไฟล์ .pyo แล้ว ใช้เป็น .pyc แทน)

สามารถทำได้ดังนี้


#python2 -m pip install cpython


ไฟล์ .pyc สามารถทำได้โดยอ่านจากบทความ compile python ไฟล์ .py

ในการแปลงเป็น .pyc ทำได้ดังนี้

สำหรับไฟล์เดียวใช้คำสั่ง python -m py_compile ไฟล์.py

สำหรับไฟล์ในโฟลเดอร์ใช้คำสั่ง python -m compileall ที่อยู่โฟลเดอร์ที่ต้องการ

ในการใช้ .pyo นั้นเพียงเติม -O หรือ -OO ไว้หลัง python

ข้อควรรู้เกี่ยวกับ -O กับ -OO


-O เป็นการปรับแต่งประสิทธิภาพ (optimized code) เบื้องต้น

-OO เป็นการปรับแต่งประสิทธิภาพ (optimized code) โดยละทิ้ง docstrings ออกไป


สำหรับไฟล์เดียวใช้คำสั่ง python -O -m py_compile ไฟล์.py

สำหรับไฟล์ในโฟลเดอร์ใช้คำสั่ง python -O -m compileall ที่อยู่โฟลเดอร์ที่ต้องการ

สมมุติเรามีไฟล์ test.py โดยมีโค้ดดังนี้

แล้วลองทำการแปลงเป็น .pyc และ .pyo โดยเปิดคอมมานด์ไลน์ใช้คำสั่ง


python -m  py_compile test.py

python -O -m  py_compile test.py

python -OO -m  py_compile test.py


จะได้โฟลเดอร์ __pycache__ ขึ้นมา โดยจะเก็บไฟล์ .pyc เอาไว้

ภายในโฟลเดอร์ __pycache__ จะพบไฟล์


test.cpython-35.pyc นี่คือ ไฟล์ .pyc ปกติ

test.cpython-35.opt-1.pyc นี่คือ ไฟล์ .pyc ที่ถูกปรับแต่ง (หรือ .pyo) โดยเติม -O

test.cpython-35.opt-2.pyc นี่คือ ไฟล์ .pyc ที่ถูกปรับแต่ง (หรือ .pyo) โดยเติม -OO

ลองทำการทดสอบความเร็วโดยใช้ time  ใน Linux วัดความเร็ว

ผลลัพธ์

ไฟล์ test.py

$ time python3 test.py

Hello! :)


real 0m0.060s

user 0m0.056s

sys 0m0.004s


ไฟล์ test.cpython-35.pyc

$ time python3 test.cpython-35.pyc

Hello! :)


real 0m0.035s

user 0m0.032s

sys 0m0.004s


ไฟล์ test.cpython-35.opt-1.pyc

$ time python3 test.cpython-35.opt-1.pyc

Hello! :)


real 0m0.034s

user 0m0.024s

sys 0m0.008s


ไฟล์ test.cpython-35.opt-2.pyc

$ time python3 test.cpython-35.opt-2.pyc

Hello! :)


real 0m0.034s

user 0m0.036s

sys 0m0.000s


จะเห็นได้ว่า พอแปลงไฟล์ .py เป็น .pyc และ .pyo จะรันได้เร็วกว่า .py

ข้อเสียคือ รันได้เฉพาะ CPython เวชั่น ระบบปฏิบัติการและสถาปัตยกรรมที่เหมือนกันเท่านั้น
