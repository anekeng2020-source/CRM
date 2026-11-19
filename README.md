# myib CRM — ระบบบริหารงานขาย (Single-file Web App)

ไฟล์เดียว `index.html` (HTML + CSS + JavaScript) เปิดด้วยเบราว์เซอร์ได้ทันที ไม่ต้องติดตั้ง
UI ใช้ design system เดียวกับ **MyIB WMS (Fusion theme)**: sidebar ลอยสีขาว, การ์ดมุมโค้ง 24px, ปุ่มทรง pill, สีส้ม `#f47a33`, ฟอนต์ Manrope + Noto Sans Thai, TH/EN, Dark mode

> ตอนนี้ข้อมูลเก็บใน `localStorage` ของเบราว์เซอร์ (โหมดทดลอง) — ยังไม่ได้ต่อฐานข้อมูลจริง

## บัญชีทดลอง
| ผู้ใช้ | รหัส | บทบาท / บริษัท |
|---|---|---|
| superadmin | super123 | Super Admin (ทุกบริษัท) |
| a1admin / a1mgr / a1sales / a1sales2 | 1234 | บริษัท A1 — โหมด **อุปกรณ์การแพทย์** |
| a2admin / a2sales / a2sales2 | 1234 | บริษัท A2 — โหมด **เครื่องมือช่าง & อุปกรณ์** |
| a3admin / a3sales | 1234 | บริษัท A3 — โหมด **งานขายทั่วไป** |

เมนูผู้ใช้ → "รีเซ็ตข้อมูลทดลอง" เพื่อเริ่มใหม่

## แหล่งอ้างอิงฟังก์ชัน
รวบรวมฟังก์ชันจาก CRM ชั้นนำ: Salesforce Sales Cloud, HubSpot CRM, Zoho CRM, Pipedrive, Microsoft Dynamics 365 Sales, Freshsales, monday CRM, Pipeliner, Zendesk Sell, Insightly
+ ฟังก์ชันเฉพาะงานขายเครื่องมือแพทย์ (Demo/Loaner, Installed base, Serial/Lot, PM/Calibration, ใบอนุญาต อย., e-Bidding)

## รายการฟังก์ชัน

### ส่วนกลาง (ทุกโหมดใช้ร่วมกัน)
| กลุ่ม | ฟังก์ชัน | อ้างอิง |
|---|---|---|
| แดชบอร์ด | KPI ไปป์ไลน์, Weighted forecast, ยอดปิดเดือนนี้ vs เป้า, Win rate 90 วัน, กราฟ 12 เดือน, Funnel ตามขั้นตอน, Leaderboard, ดีลใกล้ปิด, Widget ตามโหมด | Salesforce / HubSpot |
| ไปป์ไลน์ | Kanban ลากวาง, หลายไปป์ไลน์, % โอกาสต่อขั้น, ลากไป Won/Lost, Rotting deals (ดีลนิ่ง), กรองตามคน | Pipedrive |
| งานของฉันวันนี้ | งานเลยกำหนด/วันนี้/7 วัน, ดีลนิ่ง, ลีดถึงเวลาติดตาม, แจ้งเตือน | HubSpot Tasks / Freshsales |
| ลีด | List + Kanban, Lead scoring อัตโนมัติ, Hot/Warm/Cold, แหล่งที่มา, แคมเปญ, ตรวจข้อมูลซ้ำ, แปลงลีด → ลูกค้า + ผู้ติดต่อ + ดีล, Import/Export CSV | Salesforce / Zoho |
| ดีล | Stage bar, Won/Lost + เหตุผลที่แพ้, Weighted amount, วันนิ่ง, คู่แข่ง, สร้างใบเสนอราคาจากดีล | Salesforce Opportunity |
| ลูกค้า (Account 360°) | ไทม์ไลน์รวม, ผู้ติดต่อ/ดีล/เอกสาร/Ticket/โมดูลโหมด, Health score, ยอดซื้อสะสม, ค้างชำระ | Dynamics 365 / HubSpot |
| ผู้ติดต่อ | บทบาทการตัดสินใจ (Buying role), วันเกิด (แจ้งเตือน), LINE ID | Salesforce Contact Roles |
| กิจกรรม | โทร/ประชุม/อีเมล/งาน/เยี่ยม/สาธิต, ติ๊กเสร็จ, Log จาก drawer, โน้ต + @mention | ทุกตัว |
| ปฏิทิน | รวมกิจกรรม เยี่ยม PM ยื่นซอง คืนเครื่อง วันปิดดีล, ทีม/ของฉัน | Zoho / Pipedrive |
| อีเมล | เทมเพลต + merge fields `{{name}} {{company}} {{owner}}`, เปิดโปรแกรมอีเมล + บันทึกกิจกรรม | HubSpot Templates |
| สินค้า & ราคา | ราคา/ต้นทุน/กำไร, ฟิลด์เฉพาะโหมด, Custom fields | Zoho Price books |
| ใบเสนอราคา → ใบสั่งขาย → ใบแจ้งหนี้ | ส่วนลดรายบรรทัด/ท้ายบิล, VAT 7%, ตัวอักษรบาท, พิมพ์/PDF, สถานะ, แปลงเอกสาร, รับชำระ (บางส่วน/เต็ม), ทำสำเนา, ลูกค้าอนุมัติ → ดีลชนะ | Salesforce CPQ / Zoho |
| แคมเปญ | งบ/ค่าใช้จ่าย, ลีดจากแคมเปญ, รายได้, ROI | Salesforce Campaigns |
| Service Ticket | Kanban, ความสำคัญ, SLA, ช่องทาง | Zendesk / Freshdesk |
| รายงาน | ผลงานพนักงาน, Pipeline & Aging, Win/Loss, สินค้าขายดี, ลีด & แหล่งที่มา, กิจกรรม, ลูกค้า Top, งานบริการ — กรองช่วงวันที่ + CSV | ทุกตัว |
| พยากรณ์ | Commit / Weighted / Best case 6 เดือน, ตามพนักงาน, Coverage vs เป้า | Salesforce Forecasts |
| เป้าหมาย / Quota | ตั้งเป้ารายเดือนรายคน, % ความสำเร็จ | Pipeliner / HubSpot Goals |
| Workflow อัตโนมัติ | เมื่อ [เหตุการณ์] + [เงื่อนไข] → สร้างงาน / แจ้งเตือน / อัปเดตฟิลด์ | Salesforce Flow / HubSpot Workflows |
| ค้นหาทั้งระบบ | ลูกค้า ดีล เบอร์โทร Serial เลขเอกสาร (Ctrl+K) | ทุกตัว |
| การแจ้งเตือน | งานเลยกำหนด, ดีลนิ่ง, ยื่นซอง, เครื่องสาธิตเกินกำหนด, อย. หมดอายุ, PM, สัญญา, SLA, ใบแจ้งหนี้ค้าง, วันเกิด | — |
| ผู้ใช้ & สิทธิ์ | Admin / Manager / Sales / Viewer, ทีมขาย, จำกัดเมนูรายคน, Private records | Salesforce Profiles |
| ตั้งค่า | ข้อมูลบริษัทบนเอกสาร, VAT, ไปป์ไลน์/ขั้นตอน, Picklists, Custom fields, Backup/Restore JSON | — |
| Audit log | บันทึกสร้าง/แก้ไข/ลบ พร้อมผู้ทำและเวลา | Salesforce Field History |
| อื่นๆ | Bulk assign/delete, เลือกแสดงแถว, เรียงคอลัมน์, Quick-create ลูกค้าในฟอร์ม, มือถือ (responsive) | — |

### โหมดธุรกิจ (เมนูเปลี่ยนตามประเภทสินค้า)
| โหมด | โมดูลเฉพาะ | ฟิลด์สินค้าเฉพาะ |
|---|---|---|
| อุปกรณ์การแพทย์ | ประมูล e-Bidding (นับถอยหลังยื่นซอง, หลักประกันซอง, สร้างดีลจากงานประมูล), เครื่องสาธิต/ยืม (Demo/Loaner คืนเครื่อง), ฐานติดตั้ง Serial (ประกัน, รอบ PM), PM/Calibrate (ปิดงาน → อัปเดตรอบ PM), ใบอนุญาต อย. (แจ้งเตือนหมดอายุ) | เลข อย., Class, ยี่ห้อ, ประเทศ, ติดตาม Serial, รอบ PM |
| เครื่องมือช่าง & อุปกรณ์ | ดีลเลอร์ (Tier, เป้า/ยอด YTD), เยี่ยมลูกค้า Check-in GPS, เคลมประกัน/RMA (Kanban), เช่าเครื่องมือ, ฐานติดตั้ง | ยี่ห้อ, รุ่น, กำลังไฟ, ประกัน, ประเภท |
| ไอที & อิเล็กทรอนิกส์ | ฐานติดตั้ง, สัญญา MA (ต่ออายุ → สร้างดีล Renewal), RMA, ดีลเลอร์ | ยี่ห้อ, รุ่น, ประกัน, ไลเซนส์ |
| วัสดุก่อสร้าง | โครงการ Spec-in (Kanban ตามระยะ), ดีลเลอร์, เยี่ยมหน้างาน | ยี่ห้อ, มอก., หน่วยบรรจุ |
| สินค้าอุปโภคบริโภค | เยี่ยมร้าน (Route), ตัวแทนจำหน่าย | ยี่ห้อ, บาร์โค้ด, ขนาด, อายุสินค้า |
| งานขายทั่วไป | ใช้ฟังก์ชันส่วนกลาง | — |

### Super Admin
- ภาพรวมทุกบริษัท (Tenant), สถิติ, บันทึกระดับระบบ
- จัดการบริษัท: สร้าง/แก้ไข/ระงับ/ลบ, เลือก **โหมดธุรกิจ**, โมดูลเสริม, แพ็กเกจ (Basic/Pro/Enterprise), วันหมดอายุ, จำนวนผู้ใช้สูงสุด, Admin คนแรก, ข้อมูลตัวอย่าง
- **เปิด/ปิดโหมดธุรกิจทั้งระบบ** และ **เปิด/ปิดเมนูของแต่ละโหมด**
- เปิด/ปิดเมนูรายบริษัท, สลับเข้าดูบริษัท, ผู้ใช้ทุกบริษัท, Login as (impersonate)
- บริษัทถูกระงับ/หมดอายุ → ผู้ใช้เข้าระบบไม่ได้

ลำดับสิทธิ์เมนู: **Super Admin (โหมด) → Super Admin (บริษัท/แพ็กเกจ) → Admin บริษัท (ซ่อนจากพนักงาน) → รายผู้ใช้**

## โครงสร้างข้อมูล Multi-tenant (เหมือน MyIB WMS)
```
META = {
  companies:[{id, code, name, mode, plan, expiry, maxUsers, active, menus:{}, extraModules:[]}],
  partitions:{ <companyId>: { leads, accounts, contacts, deals, activities, notes, products,
      quotes, orders, invoices, campaigns, templates, tickets, automations, targets, audit,
      tenders, demos, installed, services, regdocs, contracts, dealers, warranty, visits,
      specprojects, rentals, settings } },
  users:[{username, password, fullName, role, company, team, menuPerms:[]}],
  modesEnabled:{}, modeMenus:{<mode>:{<menuId>:false}}
}
```
บริษัทหนึ่งอ่าน/เขียนได้เฉพาะ `partitions[companyId]` ของตัวเอง → A1 ไม่เห็นข้อมูล A2

**แผนฐานข้อมูลจริง (ขั้นต่อไป):** ทุกตารางมี `company` + `rk` (record key) + คอลัมน์ที่อ่านได้ + `data jsonb` (แบบเดียวกับ `supabase_schema.sql` ของ MyIB WMS) พร้อม RLS กรองตาม company และตาราง `companies`, `users` ระดับระบบ
