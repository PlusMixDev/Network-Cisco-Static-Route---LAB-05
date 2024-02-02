**• PART 1**

![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/f3ed6b2e-ecf7-4029-9d4e-5191a3a87f20)

**แลปนี้ให้ทำ PC0 เชื่อมต่อกับ PC1 ได้ โดยปกติแล้วเราไม่สามารถติดต่อกันข้ามเร้าเตอร์ได้ถ้าเร้าเตอร์ยังไม่รู้จักกัน**

1.ใน Packet Tracer, ใส่ Router 2621XM 2 ตัว และ ใส่ PC 2 เครื่อง. เชื่อมต่อตามรูป

	วางตามอาจารย์เลย อย่าลืมโยงสายเชื่อมต่อ (เลือกแบบอัตโนมัติ) แล้วจะได้แบบนี้ (ยังไม่ต้องสนใจชื่อ)
![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/2003b5cb-8929-45f8-b9cb-c2be9185deda)

2. เข้า CLI ของแต่ละ Router. ตั้งชื่อ Router0 ให้เป็น Router12. ตั้งชื่อ Router6 ให้เป็น Router23.
	
	เข้าไปตั้งชื่อเลย กดเข้าไปทีเร้าเตอร์แต่ละตัว แล้วตั้งชื่อ
![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/ffd8b527-26fc-43a1-a1bd-598789f60798)

	จากนั้นจะได้แบบนี้

	![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/efc7e23c-2733-4288-95fb-06119261ee49)

3. ที่ Router12, เข้า Configuration mode และ ใช้คำสั่งด้านล่าง

	กดเข้าไปที่ Router12 แถบด้านบนเลือก CLI เพื่อใช้ตั้งค่าเร้าเตอร์ แล้วพิมพ์คำสั่งตามนี้
	
	- enable (เพื่อเข้าใข้งานเร้าเตอร์)
	- config t (เพื่อเข้าสู่โหมดตั้งค่า)
	- line con 0 (ตั้งค่าคอนโซลบรรทัดแรก)
	- exec-timeout 0 0 (ให้การใช้งานไม่ต้องหลุดออกจากระบบ)
	- exit

4. แสดง Routing table ปัจจุบัน, มี entries อะไรบ้าง? อธิบายสิ่งที่ได้เจอ	(hint: show ip route)

	- อันนี้ต้องอยู่ในโหมดทั่วไปเพื่อเช็คข้อมูลทั่วไปของเร้าเตอร์ ถ้าหน้าต่างคำสั่งอยู่แบบนี้สามารถพิมพ์ได้ลย ถ้าไม่ exit ออกมาให้เป็นอันนี้

		```Router#```

		ถ้าใช่ก็ใช้คำสั่ง show ip route

		![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/207ace50-002b-4cf9-9baf-8e07a4e15473)

   	หมายความว่าเร้าเตอร์นี้ยังไม่มีการเชื่อมต่อและตั้งค่า Route เลย ในนี้จะแสดงข้อมูล Route ที่เร้าเตอร์เราไปได้ทั้งหมด

5. แสดง running configuration อธิบายสิ่งที่ได้เจอ (hint: show run)

	- ก็ไม่มีอะไร ก็แค่หน้าต่างการตั้งค่า สถานะของเร้าเตอร์ อินเตอร์เฟซ

6. แสดงข้อมูล Interface ทุก Interface ของ Router. ตรวจสอบว่าเห็นข้อมูลของทั้ง FastEthernet0/0 และ  FastEthernet0/1 หรือไม่ (hint: show interfaces)

	- ก็พิมพ์ไป กด Enter เรื่อย ๆ มันจะเลื่อนลงมาอ่านได้ ถ้าใช้เร้าเตอร์เดียวกันมันก็มีเหมือนกัน 

7. กำหนดที่อยู่ IP ของ Interface ทั้งสองเป็น 192.168.1.2 และ 192.168.2.1 โดย Subnet mask คือ 255.255.255.0

	- เรามี Interface 2 ช่อง คือ fa0/0 กับ fa0/1 ซึ่งเราจะต้องกำหนดไอพีให้ทั้งสองอัน จะสอนแบบใช้ CLI หรือคำสั่งในการทำ จะกำหนดในหน้าต่างก็ได้ ตามสะดวก
		- เข้า CLI ของ Router12
		- พิมพ์คำสั่งตามนี้
		- conf t (เข้าสู่โหมดตั้งค่า)
		- interface fa0/0 (เลือกอันเตอร์เฟซ)
		- ip address 192.168.1.2 255.255.255.0 (กำหนดไอพีให้)
		- no shutdown (ปลุกให้อินเตอร์เฟซทำงาน โดยจะเห็นว่าใน Diagram มันจะเป็นเส้นสีเขียว)
		- exit (ออกจากอินเตอร์เฟซแรก)
		
		- interface fa0/1 (เลือกอินเตอร์เฟซอันที่สอง)
		- ip address 192.168.2.1 255.255.255.0 (กำหนดไอพีให้)
		- no shutdown (ปลุกให้อินเตอร์เฟซทำงาน แต่จะเห็นว่ามันเป็นสีแดง เพราะเร้าเตอร์อีกตัวยังไม่ทำงาน ถ้ามันค้างกด Enter)
		- exit (ออกจากอินเตอร์เฟซที่สอง)

8. แสดงข้อมูล Interface ทุก Interface อีกครั้ง ตรวจสอบว่า interfaces up หรือยัง มีค่าถูกต้องตามที่กำหนดมั้ย (แนะนำ: หลังจากใช้คำสั่งแสอง interface บน command line แล้ว ให้นิสิตลองเอา Mouse ไปวางบน link ของเครือข่ายใน packet tracer ด้วย) 

	- ทำเหมือนข้อ 6

9. แสดงตาราง Routing ปัจจุบัน, มี entries อะไรบ้างแล้ว ต่างจากข้อ 4 อย่างไร?

	- อันนี้ต้องอยู่ในโหมดทั่วไปเพื่อเช็คข้อมูลทั่วไปของเร้าเตอร์ ถ้าหน้าต่างคำสั่งอยู่แบบนี้สามารถพิมพ์ได้ลย ถ้าไม่ exit ออกมาให้เป็นอันนี้

		```Router#```

		ถ้าใช่ก็ใช้คำสั่ง show ip route

		![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/da2e9f86-2327-40f5-ba01-7f2588034f5e)

   	หมายความว่า อินเตอร์เฟซที่เราเปิดเมื่อกี้ สามารถเชื่อมต่อไปหาคอมพิวเตอร์ติดแล้ว แต่อีกอีกสายนึงที่ต่อไปยังอีกเร้าเตอร์ไม่ติด เพราะว่ายังไม่ได้เปิดใช้งาน

10. แสดง running configuration อธิบายสิ่งที่ได้เจอ ดูว่าต่างจากข้อ 5 มั้ย

	- ต่างอยู่แล้ว เพราะมีการตั้งไอพีให้อินเตอร์เฟซเพิ่ม ซึ่งข้อมูลของแต่ละอินเตอร์เฟซจะมีไอพีของตัวเองแล้ว

11. ทำซ้ำข้อ 2-10 กับ Router23 โดยกำหนดที่อยู่ IP ให้เป็น 192.168.2.2 and 192.168.3.1 และ Subnet mask เป็น 255.255.255.0

	กดเข้าไปที่ Router23 แถบด้านบนเลือก CLI เพื่อใช้ตั้งค่าเร้าเตอร์ แล้วพิมพ์คำสั่งตามนี้
	
	- enable (เพื่อเข้าใข้งานเร้าเตอร์)
	- config t (เพื่อเข้าสู่โหมดตั้งค่า)
	- line con 0 (ตั้งค่าคอนโซลบรรทัดแรก)
	- exec-timeout 0 0 (ให้การใช้งานไม่ต้องหลุดออกจากระบบ)
	- exit

	จากนั้นเราจะตั้งไอพีให้อินเตอร์เฟซกัน

	- interface fa0/0 (เลือกอันเตอร์เฟซ)
	- ip address 192.168.2.1 255.255.255.0 (กำหนดไอพีให้)
	- no shutdown (ปลุกให้อินเตอร์เฟซทำงาน โดยจะเห็นว่าใน Diagram มันจะเป็นเส้นสีเขียว)
	- exit (ออกจากอินเตอร์เฟซแรก)
		
	- interface fa0/1 (เลือกอินเตอร์เฟซอันที่สอง)
	- ip address 192.168.3.1 255.255.255.0 (กำหนดไอพีให้)
	- no shutdown (ปลุกให้อินเตอร์เฟซทำงาน แต่จะเห็นว่ามันเป็นสีแดง เพราะเร้าเตอร์อีกตัวยังไม่ทำงาน ถ้ามันค้างกด Enter)
	- exit (ออกจากอินเตอร์เฟซที่สอง)

	ทีนี้ทั้งหมดก็จะเขียว เพราะว่าไฟต่อหากันติดแล้ว แต่ว่ายังไม่เชื่อมต่อกันไม่ติด

12. ไปที่ PC ซ้ายมือที่อยู่ใน Subnet 192.168.1.0 เปลี่ยนชื่อมันเป็น PC11 กำหนดที่อยู่ IP เป็น 192.168.1.1 (แนะนำ : อย่าลืมตั้ง Gateway ด้วย)
	
	- เข้าไปเลย แล้วตั้งตามนี้ ทั้งหมวด Settings แล้วก็ FastEthernet0

	![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/56e1ac12-090d-450e-8590-a7ed4f41819d)

	![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/fdbf0b78-4075-4347-bad0-dad9d94e8692)

	ที่เราตั้ง Gateway ไปที่ 192.168.1.2 ให้เรามองว่ามันต้องเชื่อมกับ Router12 เราเลยให้มันเป็น Gateway นี้

13. ไปที่ PC ขวามือที่อยู่ใน Subnet 192.168.3.0 เปลี่ยนชื่อมันเป็น PC33 กำหนดที่อยู่ IP เป็น 192.168.3.2

	- เข้าไปเลย แล้วตั้งตามนี้ ทั้งหมวด Settings แล้วก็ FastEthernet0

	![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/1cde8f2c-f70b-43ba-8b7a-26cc9caea2b8)

	![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/b539455f-1a3e-480e-98d8-eedf5e47ee88)

	ที่เราตั้ง Gateway ไปที่ 192.168.3.1 ให้เรามองว่ามันต้องเชื่อมกับ Router23 เราเลยให้มันเป็น Gateway นี้
	
14. Ping จาก PC11 ไปยัง PC33. เกิดอะไรขึ้น เพราะอะไร ?
	- เรากลับไปที่ PC11 แล้ว เข้าหมวดหมู่ Desktop แล้วเลือก Command Prompt ซึ่งมันคือนหน้าต่างไว้พิมพ์คำสั่ง
	
	![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/de63ed6c-6709-46d5-a7a9-c45e3f3d80c5)

	![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/0c73cf09-2ad2-40c5-83cb-8c879f06719e)

	- จากนั้นก็ปิงเลย ping 192.168.3.2 (กด CTRL C ยกเลิก)

	![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/6d3083de-4043-4429-a0e0-265c6ef8d6e0)

	จะเห็นว่ามันขึ้น Host Unreachable แปลว่าเร้าเตอร์ไม่รู้จักเครื่องปลายทาง

15. เพิ่ม static route ให้กับ Router12 and Router23.

	- Route คือการที่เครื่องเร้าเตอร์หรือคอมมันรู้จักกับเครือข่ายอีกอันนึงได้ มันจึงรู้ว่ามันต้องส่งไปทางไหน
	- Route จะสร้างโดยอัตโนมัติ ถ้าทั้งสองอันเชื่อมต่อกันโดยตตรง เช่น PC11 ต่อกับ Router12 ซึ่งเราสามารถปิงจาก PC11 ไป Router12 ได้

		![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/424fb00e-c6d2-4e90-b53d-19d776ee5dd5)

	- แต่ถ้าไม่ได้ต่อกันโดยตรง แล้วไม่มีข้อมูล Route เราจะไม่สามารถสื่อสารกับอีกเครื่องได้เหมือนกรณีปิงจาก PC11 ไป PC33 รวมถึง PC11 ก็ปิงไปหา Router23 ไม่ได้เพราะไม่ได้เชื่อมต่อกันโดยตรง

		![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/ca1b5176-5c1f-4897-bc3b-d4bc92af8b28)

	- ดังนั้นเราจึงต้องสร้าง Route โดยจะคิดตามแพทเทิร์นแบบนี้

	- ถ้าเราอยากให้ปิงจาก PC11 ไป PC33 ได้ เราต้องตั้งค่าเร้าเตอร์ของ PC11 นั่นคือ Router12 ให้รู้ว่า PC33 อยู่ที่ไหน
	- ซึ่ง PC33 อยู่ภายใต้ Router23 ดังนั้นเราต้องบอก Router12 ว่า PC33 อยู่ใน Router23
	- ซึ่งแพทเทิร์นคำสั่งจะเป็นแบบนี้ | ip route ไอพีเครื่องที่ต่อไม่ติด(เปลี่ยนเลขสุดท้ายเป็น0) subnetmask ไอพีเร้าเตอร์ที่เครื่องนั้นอยู่
			
	( ที่เปลี่ยนเลขสุดท้ายเป็น 0 เพราะว่าเราต้องการให้ทั้งวงไอพีของเครื่องปลายทาง หมายถึงทุกเครื่องที่เชื่อมต่ออยู่ใน Router นั้น ๆ สามารถติดต่อกับเราได้ )
			
	- เข้าไปที่ Router12 แล้วเข้าหน้า CLI เหมือนเดิมแล้ว มั่นใจว่าตรงที่พิมพ์คำสั่งต้องเป็นแบบนี้

 		```Router#```

	- ถ้ามันเกิดเป็น Router> ให้พิมพ์คำสั่ง enable ถ้าถูกแล้วเริ่มพิมพ์คำสั่งเลย
	- config t
	- ip route 192.168.3.0 255.255.255.0 192.168.3.1
   	- exit
    - show ip route (จะเห็นว่ามันมี Static Route เพิ่มขึ้นมา )
		![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/bee91688-18f0-4b84-a207-98c55142d1a3)
	- ต่อไปจะไปทำให้ PC33 ต่อมาที่ PC11 ได้บ้าง
	- เข้าไปที่ Router12 แล้วเข้าหน้า CLI เหมือนเดิมแล้ว มั่นใจว่าตรงที่พิมพ์คำสั่งต้องเป็นแบบนี้

 		```Router#```

	- ถ้ามันเกิดเป็น Router> ให้พิมพ์คำสั่ง enable ถ้าถูกแล้วเริ่มพิมพ์คำสั่งเลย
	- config t
	- ip route 192.168.3.0 255.255.255.0 192.168.3.1
    - exit
    - show ip route (จะเห็นว่ามันมี Static Route เพิ่มขึ้นมา )
		![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/0ef54601-3bac-43fb-8a83-451de4e4442d)


	แค่นี้ก็เสร็จสิ้นการทำ Static Route

16. Ping จาก PC11 ไปยัง PC33. เกิดอะไรขึ้น เพราะอะไร ?
	
	ปิงติดแล้ว เพราะว่าเราทำ Route เรียบร้อยแล้วซึ่งเครือข่ายทั้งสองก็สามารถติดต่อข้ามกันได้แล้ว

	![image](https://github.com/PlusMixDev/Network-Cisco-Static-Route-LAB05/assets/54778209/c4e4e5c1-4f24-4bc2-a3b0-641a7389293f)

			
