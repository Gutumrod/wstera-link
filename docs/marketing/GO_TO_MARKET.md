# WSTERA Link — Go-To-Market Plan

**Status:** LOCKED launch-preparation baseline  
**Date:** 2026-08-26

## GTM Objective
หา users กลุ่มแรกที่มี traffic จริงและใช้ลิงก์ในงานจริง เพื่อพิสูจน์ activation, repeat usage และ willingness to pay ก่อนขยายตลาด

## Beachhead Market
เริ่มจากไทยก่อน โดยโฟกัส:
1. ร้านค้าออนไลน์และเพจขายของ
2. Creator / affiliate operator
3. ร้านบริการที่ใช้ QR หรือ social links
4. Agency/social admin ขนาดเล็ก

ไม่เปิด positioning แบบ “ทุกคนที่ต้องการย่อลิงก์” ในช่วงแรก

## Acquisition Order
### Channel 1 — WSTERA Internal Dogfooding
ใช้ WSTERA products และทรัพย์สินที่ควบคุมเองสร้าง real traffic / failure evidence / case study

### Channel 2 — Friendly Businesses / Pilot Customers
ร้านที่มี social traffic จริงและยอมให้วัดผลก่อน-หลัง

### Channel 3 — Seller / Creator Communities
แจก use case และ analytics examples ไม่ขายด้วย feature list อย่างเดียว

### Channel 4 — Content / SEO
เนื้อหาแนว “รู้ได้อย่างไรว่าลูกค้ามาจากโพสต์ไหน”, “QR เดิมแต่เปลี่ยนปลายทาง”, “วัด affiliate outbound clicks”

### Channel 5 — Referral / Agency
หลัง workflow stable จึงทำ referral หรือ agency-oriented acquisition

## First 100 Tenant Strategy
- 10 internal/friendly pilot tenants
- 20 closed-beta tenants
- 20 paid-beta tenants
- 50 public early adopters

จำนวนเป็น planning target ไม่ใช่ success guarantee; Launch Plan เป็นผู้กำหนด gate จริง

## Offer Strategy
### Free
ใช้พิสูจน์ first value: link → real click → analytics

### Pro
default paid plan สำหรับร้าน/creator จริง

### Business
สำหรับทีม, API/webhook และ volume สูงกว่า

ไม่ใช้ permanent discount เป็น core positioning

## Case Study Template
ทุก case study ต้องมี:
- Customer type
- Problem before WSTERA Link
- Channel/link setup
- Real measurement period
- Outcome with evidence
- Limitation / what was not measured
- Permission to publish

## Sales Narrative
1. คุณโพสต์หลายช่องไหม?
2. ตอนนี้รู้ไหมว่าคลิกมาจากช่องไหน?
3. ถ้า QR หรือโพสต์เก่าเปลี่ยนปลายทาง ต้องแก้ของเดิมไหม?
4. WSTERA Link ให้ stable link + source analytics + dynamic destination
5. เริ่ม Free และ upgrade เมื่อ traffic/feature โต

## Funnel
Visitor → Signup → First Link → First Real Click → Return to Analytics → Second Link/Campaign → Limit/Paid Feature Need → Upgrade

## Activation Target Definition
Activated tenant = tenant ที่สร้าง link สำเร็จและได้รับ tracked click จริงอย่างน้อย 1 ครั้ง

## Feedback Loop
ทุก Beta cohort เก็บ:
- ทำไมสมัคร
- ใช้ลิงก์ที่ไหน
- เข้าใจ analytics หรือไม่
- feature ที่ block งานจริง
- เหตุผลที่จ่าย/ไม่จ่าย
- bug/reliability friction

Feedback ที่เปลี่ยน scope ต้องผ่าน ADR ก่อนแก้ Product Truth

## GTM Readiness Checklist
- [ ] Stable signup/create-link flow
- [ ] Real redirect traffic ผ่าน Phase 3
- [ ] Analytics อธิบายง่าย
- [ ] Pricing page ตรง entitlement จริง
- [ ] Privacy/Terms พร้อมก่อน external public users
- [ ] Support/contact channel พร้อม
- [ ] Incident response owner พร้อม
- [ ] Case-study consent process พร้อม

## Stop Conditions
หยุดขยาย acquisition ถ้า:
- มี cross-tenant/security incident
- redirect reliability ยังไม่ผ่าน gate
- quota/billing behavior ไม่ตรงเอกสาร
- privacy/legal requirement blocking ยังไม่ปิด
