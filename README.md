<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>ระบบใบงานและแบบฝึกหัดออนไลน์ (หลายรายวิชา)</title>
    <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #2980b9;
            --primary-dark: #2471a3;
            --secondary: #2ecc71;
            --secondary-dark: #27ae60;
            --accent: #e67e22;
            --bg-color: #f0f4f8;
            --text-main: #333;
            --border: #d1d8e0;
        }

        body {
            font-family: 'Sarabun', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
        }

        .container {
            background-color: #fff;
            width: 100%;
            max-width: 900px;
            border-radius: 12px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.05);
            overflow: hidden;
            position: relative;
        }

        .header {
            background-color: var(--primary);
            color: white;
            padding: 25px 20px;
            text-align: center;
            position: relative;
        }

        .header h1 { margin: 0; font-size: 26px; }
        .header p { margin: 5px 0 0 0; opacity: 0.9; }

        .content { padding: 30px; }

        /* Forms & Inputs */
        .form-group { margin-bottom: 25px; padding: 15px; background: #fdfdfd; border: 1px solid #eee; border-radius: 10px; }
        .form-group label {
            display: block;
            font-weight: 700;
            margin-bottom: 12px;
            color: var(--primary-dark);
            font-size: 17px;
        }
        input[type="text"], textarea, input[type="number"], select {
            width: 100%;
            padding: 12px;
            border: 2px solid var(--border);
            border-radius: 8px;
            font-family: 'Sarabun', sans-serif;
            font-size: 16px;
            box-sizing: border-box;
            transition: border-color 0.3s;
            background-color: #fff;
        }
        input[type="text"]:focus, textarea:focus, input[type="number"]:focus, select:focus {
            outline: none;
            border-color: var(--primary);
        }
        .readonly-input { background-color: #e9ecef !important; color: #6c757d; cursor: not-allowed; }

        /* Custom Input Types */
        .checkbox-group, .radio-group { display: flex; flex-direction: column; gap: 10px; }
        .checkbox-group label, .radio-group label { font-weight: normal; color: #333; display: flex; align-items: center; font-size: 16px; margin-bottom: 0;}
        .checkbox-group input, .radio-group input { margin-right: 10px; transform: scale(1.2); }
        
        .sort-list { list-style: none; padding: 0; margin: 0; }
        .sort-list li { background: #fff; border: 1px solid #ccc; padding: 10px 15px; margin-bottom: 8px; border-radius: 6px; display: flex; justify-content: space-between; align-items: center; box-shadow: 0 2px 4px rgba(0,0,0,0.02);}
        .sort-btn-group button { background: #eee; border: 1px solid #ddd; border-radius: 4px; padding: 5px 10px; cursor: pointer; font-size: 14px; margin-left: 5px;}
        .sort-btn-group button:active { background: #ddd; }

        .match-row { display: flex; align-items: center; gap: 15px; margin-bottom: 10px; }
        .match-left { flex: 1; padding: 10px; background: #e8f4f8; border-radius: 6px; font-weight: bold; text-align: center; border: 1px solid #b3d4fc;}
        .match-right { flex: 1; }

        .media-container { text-align: center; margin-bottom: 15px; background: #000; border-radius: 8px; overflow: hidden; }
        .media-container img, .media-container video { max-width: 100%; height: auto; display: block; margin: 0 auto; }
        .media-container iframe { width: 100%; aspect-ratio: 16/9; border: none; }
        .media-audio { background: #f1f3f4; padding: 15px; border-radius: 8px; text-align: center; }

        .voice-record-btn { background: #e74c3c; color: white; border: none; padding: 10px 20px; border-radius: 20px; font-family: 'Sarabun'; cursor: pointer; display: flex; align-items: center; gap: 8px; font-weight: bold; margin-bottom: 10px;}
        .voice-record-btn.recording { animation: pulse 1.5s infinite; background: #c0392b; }
        @keyframes pulse { 0% { transform: scale(1); } 50% { transform: scale(1.05); } 100% { transform: scale(1); } }

        /* Buttons */
        .btn { display: inline-flex; align-items: center; justify-content: center; gap: 8px; background-color: var(--primary); color: white; padding: 12px 24px; border: none; border-radius: 8px; font-size: 16px; font-family: 'Sarabun', sans-serif; font-weight: bold; cursor: pointer; transition: all 0.2s; width: 100%; box-sizing: border-box; }
        .btn:hover { background-color: var(--primary-dark); transform: translateY(-2px); }
        .btn:active { transform: translateY(0); }
        .btn-success { background-color: var(--secondary); }
        .btn-success:hover { background-color: var(--secondary-dark); }
        .btn-outline { background-color: transparent; border: 2px solid var(--primary); color: var(--primary); }
        .btn-outline:hover { background-color: var(--primary); color: white; }
        .btn-capture { background-color: #9b59b6; color: white; border: none; }
        .btn-capture:hover { background-color: #8e44ad; }
        .btn-back { position: absolute; left: 20px; top: 25px; background: rgba(255,255,255,0.2); color: white; border: none; padding: 8px 15px; border-radius: 6px; cursor: pointer; font-family: 'Sarabun'; font-weight: bold; }
        .btn-back:hover { background: rgba(255,255,255,0.3); }

        .button-group { display: flex; gap: 15px; margin-top: 30px; }

        /* Screens */
        .screen { display: none; }
        .screen.active { display: block; animation: fadeIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(15px); } to { opacity: 1; transform: translateY(0); } }

        /* Loading Screen */
        .loader-spinner { border: 5px solid #f3f3f3; border-top: 5px solid var(--primary); border-radius: 50%; width: 50px; height: 50px; animation: spin 1s linear infinite; margin: 0 auto 20px auto; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        /* Grid for Subjects and Dashboard */
        .grid-container { display: grid; grid-template-columns: repeat(auto-fill, minmax(350px, 1fr)); gap: 20px; }
        .card { border: 2px solid var(--border); border-radius: 10px; padding: 20px; display: flex; flex-direction: column; justify-content: space-between; background: #fafafa; transition: border-color 0.3s, box-shadow 0.3s, transform 0.2s; }
        .card:hover { border-color: var(--primary); box-shadow: 0 4px 12px rgba(41, 128, 185, 0.1); }
        .card.subject-card:hover { transform: translateY(-5px); border-color: var(--accent); box-shadow: 0 6px 15px rgba(230, 126, 34, 0.2); }
        .card-info h3 { margin: 0 0 8px 0; color: var(--primary-dark); font-size: 18px; }
        .card-info p { margin: 0 0 15px 0; color: #666; font-size: 14px; line-height: 1.5; }
        .card-footer { display: flex; justify-content: space-between; align-items: center; border-top: 1px dashed #ddd; padding-top: 15px; }
        .status-badge { padding: 6px 12px; border-radius: 20px; font-size: 13px; font-weight: bold; }
        .status-incomplete { background: #ffeaa7; color: #d35400; }
        .status-complete { background: #55efc4; color: #00b894; }

        /* Canvas */
        .canvas-container { border: 2px dashed var(--primary); border-radius: 8px; margin-bottom: 10px; background: #fff; position: relative; }
        canvas { display: block; width: 100%; border-radius: 8px; cursor: crosshair; touch-action: none; }
        .canvas-tools { display: flex; justify-content: flex-end; margin-bottom: 10px; }
        .btn-small { padding: 6px 12px; font-size: 14px; width: auto; }

        /* User Bar */
        .user-bar { background: #ecf0f1; padding: 12px 25px; display: flex; justify-content: space-between; align-items: center; font-weight: bold; font-size: 15px; border-bottom: 1px solid #ddd; }
        .logout-link { color: #e74c3c; text-decoration: none; cursor: pointer; transition: color 0.2s;}
        .logout-link:hover { color: #c0392b; text-decoration: underline; }

        /* Custom Alert and Confirm */
        .custom-alert-overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); z-index: 9999; justify-content: center; align-items: center; }
        .custom-alert-box { background: white; padding: 40px; border-radius: 15px; text-align: center; border: 6px solid #e74c3c; box-shadow: 0 10px 30px rgba(0,0,0,0.5); animation: popShake 0.4s ease-out; max-width: 90%; }
        .custom-alert-box h2 { font-size: 28px; margin: 0 0 20px 0; text-shadow: 1px 1px 3px rgba(0,0,0,0.1); }
        @keyframes popShake { 0% { transform: scale(0.8) translateX(0); opacity: 0; } 25% { transform: scale(1.05) translateX(-10px); opacity: 1; } 50% { transform: scale(1) translateX(10px); } 75% { transform: scale(1) translateX(-10px); } 100% { transform: scale(1) translateX(0); } }

        /* Responsive */
        @media (max-width: 820px) {
            body { padding: 10px; }
            .container { width: 100%; box-sizing: border-box; }
            .header h1 { font-size: 22px; }
            .content { padding: 20px; }
            .btn-back { top: 15px; position: static; display: inline-block; margin-bottom: 10px; }
        }

        @media (max-width: 600px) {
            .grid-container { grid-template-columns: 1fr; }
            .button-group { flex-direction: column; gap: 10px; }
            .button-group .btn { width: 100%; margin-bottom: 0; }
            .card-footer { flex-direction: column; gap: 15px; align-items: flex-start;}
            .card-footer .btn { width: 100%; }
            #screen-login .form-group[style*="display: flex"] { flex-direction: column !important; gap: 15px !important; }
            .card-info h3 { font-size: 16px; }
            .user-bar { flex-direction: column; gap: 10px; text-align: center; }
            .custom-alert-box h2 { font-size: 22px; }
            .match-row { flex-direction: column; gap: 5px; }
            .match-left { width: 100%; box-sizing: border-box; }
        }
    </style>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
</head>
<body>

<div class="container">
    
    <!-- หน้าจอโหลดข้อมูล (Loading Screen) -->
    <div id="screen-loading" class="screen active">
        <div class="content" style="text-align: center; padding: 100px 20px;">
            <div class="loader-spinner"></div>
            <h2 style="color: var(--primary);">กำลังเตรียมระบบและซิงค์ข้อมูล...</h2>
            <p style="color: #666;">กรุณารอสักครู่ ระบบกำลังโหลดใบงาน</p>
        </div>
    </div>

    <!-- หน้าเลือกรายวิชา -->
    <div id="screen-subjects" class="screen">
        <div class="header">
            <!-- ปุ่มลับสำหรับครูไว้ใช้งาน AI Worksheet Generator -->
            <button class="btn-outline" style="position: absolute; right: 20px; top: 25px; border-color: rgba(255,255,255,0.5); color: white; padding: 8px 15px; font-size: 14px;" onclick="openTeacherAdmin()">👨‍🏫 เครื่องมือครู</button>
            
            <h1>📚 เลือกรายวิชาที่ต้องการเรียน</h1>
            <p>คลิกเลือกรายวิชาเพื่อทำการล็อกอินเข้าสู่ระบบ</p>
        </div>
        <div class="content">
            <div class="grid-container" id="subjects-container"></div>
        </div>
    </div>

    <!-- หน้าเข้าสู่ระบบ -->
    <div id="screen-login" class="screen">
        <div class="header">
            <button class="btn-back" onclick="showScreen('screen-subjects')">⬅️ กลับ</button>
            <h1 id="login-subject-title">🏫 เข้าสู่ระบบ</h1>
            <p>กรุณากรอกข้อมูลเพื่อเข้าทำแบบฝึกหัด</p>
        </div>
        <div class="content" style="max-width: 500px; margin: 0 auto;">
            <div style="background: #e8f4f8; padding: 15px; border-radius: 8px; margin-bottom: 25px; font-size: 14px; border-left: 4px solid var(--primary);">
                💡 <strong>คำแนะนำ:</strong> กรุณากรอกรหัสประจำตัวนักเรียน ระบบจะค้นหาและดึงข้อมูลจากฐานข้อมูลของโรงเรียนมาให้อัตโนมัติ
            </div>
            <div class="form-group" style="border:none; padding:0; background:transparent;">
                <label>รหัสประจำตัวนักเรียน*</label>
                <input type="number" id="login-id" placeholder="พิมพ์รหัสที่นี่..." autocomplete="off" oninput="checkStudentId()">
            </div>
            <div class="form-group" style="border:none; padding:0; background:transparent;">
                <label>ชื่อ - นามสกุล</label>
                <input type="text" id="login-name" class="readonly-input" placeholder="ระบบจะกรอกอัตโนมัติ" readonly>
            </div>
            <div class="form-group" style="display: flex; gap: 15px; border:none; padding:0; background:transparent;">
                <div style="flex: 1;">
                    <label>ชั้น</label>
                    <input type="text" id="login-class" class="readonly-input" placeholder="อัตโนมัติ" readonly>
                </div>
                <div style="flex: 1;">
                    <label>เลขที่</label>
                    <input type="number" id="login-roll" class="readonly-input" placeholder="อัตโนมัติ" readonly>
                </div>
            </div>
            <button class="btn" onclick="handleLogin()" style="margin-top: 15px; font-size: 18px;">เข้าสู่ระบบ</button>
        </div>
    </div>

    <!-- แถบข้อมูลผู้ใช้ -->
    <div id="user-bar" class="user-bar" style="display: none;">
        <span id="display-user-info">ผู้ใช้งาน: -</span>
        <span class="logout-link" onclick="handleLogout()">🚪 เปลี่ยนวิชา</span>
    </div>

    <!-- หน้าแดชบอร์ดใบงานของวิชานั้นๆ -->
    <div id="screen-dashboard" class="screen">
        <div class="header">
            <h1 id="dashboard-subject-title">ชื่อวิชา</h1>
            <p>เลือกใบงานที่ต้องการทำ</p>
        </div>
        <div class="content">
            <div class="grid-container" id="dashboard-container"></div>
        </div>
    </div>

    <!-- หน้าทำใบงาน -->
    <div id="screen-worksheet" class="screen">
        <!-- เนื้อหาใบงานจะแสดงที่นี่ -->
    </div>

    <!-- หน้าเครื่องมือครู (AI Worksheet Generator) -->
    <div id="screen-teacher-admin" class="screen">
        <div class="header" style="background-color: #8e44ad;">
            <button class="btn-back" onclick="showScreen('screen-subjects')">⬅️ กลับหน้าหลัก</button>
            <h1>🤖 เครื่องมือสร้างใบงานด้วย AI</h1>
            <p>ประหยัดเวลาครู ให้ AI ช่วยเขียนโครงสร้างใบงาน</p>
        </div>
        <div class="content" style="max-width: 700px; margin: 0 auto;">
            <div style="background: #fdfdfd; padding: 25px; border-radius: 10px; border: 2px solid #9b59b6;">
                <h3 style="color: #8e44ad; margin-top:0;">✨ สั่ง AI สร้างใบงานอัจฉริยะ</h3>
                <p style="color: #666; font-size: 15px; margin-bottom: 15px;">
                    พิมพ์เนื้อหาหรือหัวข้อที่ต้องการสั่งให้ AI ทำ (ยิ่งระบุรูปแบบข้อสอบชัดเจน ยิ่งได้ผลลัพธ์ที่แม่นยำ)
                </p>
                <textarea id="ai-prompt-input" rows="4" placeholder="ตัวอย่างการสั่ง: สร้างข้อสอบวิทยาศาสตร์ ม.1 เรื่องเซลล์พืชและสัตว์ ประกอบด้วย: ปรนัย 3 ข้อ, จับคู่ 2 ข้อ และให้นักเรียนวาดรูป 1 ข้อ"></textarea>
                
                <button id="generate-ai-btn" class="btn" style="background-color: #9b59b6; margin-top: 15px; width: 100%;" onclick="generateWorksheetWithAI()">
                    ✨ ให้ AI สร้างโค้ดคำถามเดี๋ยวนี้
                </button>
                
                <div style="margin-top: 25px; border-top: 1px dashed #ccc; padding-top: 15px;">
                    <label style="font-weight: bold; color: #2c3e50;">📋 ผลลัพธ์จาก AI (คัดลอกไปวางใน Google Sheets คอลัมน์ G ได้เลย)</label>
                    <textarea id="ai-output-result" rows="6" style="background: #f4f4f4; color: #333; font-family: monospace; font-size: 14px; margin-top: 10px;" readonly placeholder="รอการประมวลผล..."></textarea>
                    <button class="btn btn-outline btn-small" style="margin-top: 10px; width: 100%; border-color: #8e44ad; color: #8e44ad;" onclick="copyAIOutput()">📋 คัดลอกข้อความทั้งหมด</button>
                </div>
            </div>
        </div>
    </div>

</div>

<!-- กล่องแจ้งเตือน (Custom Alert) -->
<div id="custom-alert-overlay" class="custom-alert-overlay">
    <div id="custom-alert-box" class="custom-alert-box">
        <h2 id="custom-alert-title">⚠️ แจ้งเตือน</h2>
        <button id="custom-alert-btn" class="btn btn-outline" style="font-size: 20px; padding: 10px 40px; border-color: #e74c3c; color: #e74c3c;" onclick="closeCustomAlert()">ตกลง</button>
    </div>
</div>

<!-- กล่องยืนยันการดำเนินการ (Custom Confirm) -->
<div id="custom-confirm-overlay" class="custom-alert-overlay">
    <div class="custom-alert-box" style="border-color: #e67e22;">
        <h2 id="confirm-title" style="color: #e67e22; font-size: 28px;">⚠️ ยืนยันการดำเนินการ</h2>
        <p id="confirm-message" style="color: #666; margin-bottom: 20px; font-size: 16px;">คุณแน่ใจหรือไม่?</p>
        <div class="button-group" style="justify-content: center; margin-top: 0; flex-direction: row;">
            <button class="btn btn-outline" style="border-color: #7f8c8d; color: #7f8c8d; width: auto;" onclick="closeCustomConfirm()">ยกเลิก</button>
            <button class="btn" id="confirm-yes-btn" style="background-color: #e67e22; width: auto;" onclick="executeConfirm()">ยืนยัน</button>
        </div>
    </div>
</div>

<!-- กล่องใส่รหัสผ่านครู -->
<div id="teacher-password-overlay" class="custom-alert-overlay">
    <div class="custom-alert-box" style="border-color: #8e44ad;">
        <h2 style="color: #8e44ad; font-size: 28px;">🔒 รหัสผ่านสำหรับครู</h2>
        <p style="color: #666; margin-bottom: 15px;">กรุณากรอกรหัสผ่านเพื่อเข้าสู่เครื่องมือครู</p>
        <input type="password" id="teacher-pwd-input" placeholder="พิมพ์รหัสผ่าน (1234)" style="text-align:center; margin-bottom: 10px; font-size: 20px;">
        <p id="teacher-pwd-error" style="color: #e74c3c; margin: 0 0 15px 0; display: none; font-size: 14px;">❌ รหัสผ่านไม่ถูกต้อง!</p>
        <div class="button-group" style="justify-content: center; margin-top: 0; flex-direction: row;">
            <button class="btn btn-outline" style="border-color: #7f8c8d; color: #7f8c8d; width: auto;" onclick="closeTeacherPassword()">ยกเลิก</button>
            <button class="btn" style="background-color: #8e44ad; width: auto;" onclick="verifyTeacherPassword()">ยืนยัน</button>
        </div>
    </div>
</div>

<script>
    // ==========================================
    // ⚙️ การตั้งค่า GOOGLE SHEETS API และ AI
    // ==========================================
    const GOOGLE_SHEET_API_URL = ""; 
    
    // 🔑 API Key สำหรับ Gemini AI (AI Worksheet Generator)
    // ⚠️ สำคัญ: หากคุณครูนำไฟล์นี้ไปใช้งานนอกระบบ (เช่น ไปสร้างเว็บเองบน Tiiny.host หรือฝังในหน้าเว็บโรงเรียน)
    // คุณครูต้องนำ API Key ของ Google Gemini มาใส่ในเครื่องหมายฟันหนูด้านล่างนี้ ระบบ AI จึงจะทำงานได้ครับ
    // (ขอรับ API Key ฟรีได้ที่: https://aistudio.google.com/app/apikey)
    const apiKey = "AQ.Ab8RN6LrRdONCkTOg_fHIAs89Mx9zFRNPbEWFTj4FnhQ2iU4Rg"; 

    let allSubjects = [];
    let studentDB = {};

    // ==========================================
    // 💡 ข้อมูลสาธิต & โครงสร้าง 22 ใบงาน ม.1
    // ==========================================
    const DEMO_DATA = {
        students: {
            "10001": { name: "ด.ช. สมชาย รักเรียน", class: "ม.1/1", roll: 1 },
            "10002": { name: "ด.ญ. สมหญิง จริงใจ", class: "ม.1/1", roll: 2 }
        },
        subjects: [
            {
                id: "subj_cs_m1", name: "💻 วิทยาการคำนวณ ม.1", desc: "รวมใบงานวิชาวิทยาการคำนวณ จำนวน 22 ใบงาน (อ้างอิง สสวท.)",
                worksheets: [
                    {
                        id: 'cs_ws1', title: 'กิจกรรมที่ 1.1 เรื่อง บ้านในฝัน', desc: 'ให้นักเรียนวาดรูปบ้านในจินตนาการและเปรียบเทียบกับเพื่อน',
                        questions: [
                            'draw::1. ให้นักเรียนวาดรูปบ้านในจินตนาการของตนเองลงในกรอบด้านล่าง',
                            'text::2.1 สิ่งที่เหมือนกัน (ระหว่างบ้านตัวเองและเพื่อน) คือ:',
                            'text::2.2 สิ่งที่แตกต่างกัน คือ:',
                            'text::3. ให้จัดกลุ่มรูปบ้านของนักเรียนทั้งห้อง นักเรียนจะใช้เกณฑ์อะไรในการจัดกลุ่ม:'
                        ]
                    },
                    {
                        id: 'cs_ws2', title: 'กิจกรรมที่ 1.2 เรื่อง สิ่งไหนจำเป็นบ้างนะ', desc: 'วิเคราะห์สถานการณ์ แล้วบอกว่าข้อมูลใดจำเป็นในการทำงาน พร้อมอธิบายเหตุผล',
                        questions: [
                            'text::1. การเดินทางจากบ้านไปโรงเรียน ข้อมูลที่จำเป็น คือ:',
                            'text::2. การเลือกซื้อสินค้า ข้อมูลที่จำเป็น คือ:',
                            'text::3. การเลือกรับประทานอาหาร ข้อมูลที่จำเป็น คือ:',
                            'text::4. การทำไข่เจียว ข้อมูลที่จำเป็น คือ:',
                            'text::5. การวาดรูปต้นไม้หรือดอกไม้ ข้อมูลที่จำเป็น คือ:'
                        ]
                    },
                    {
                        id: 'cs_ws3', title: 'กิจกรรมที่ 1.3 เรื่อง สิ่งใดเป็นข้อมูลที่จำเป็นและไม่จำเป็น', desc: 'พิจารณาสถานการณ์ว่ามีสิ่งใดเป็นข้อมูลที่จำเป็น และไม่จำเป็นต่อการแก้ปัญหา',
                        questions: [
                            'text::1. ให้นักเรียนพิจารณาสถานการณ์ที่กำหนด ข้อมูลที่จำเป็นต่อการแก้ปัญหาคืออะไร พร้อมแสดงวิธีหาคำตอบ:'
                        ]
                    },
                    { id: 'cs_ws4', title: 'กิจกรรมที่ 1.4 การรวบรวมข้อมูล', desc: 'ให้นักเรียนอธิบายวิธีการรวบรวมข้อมูลที่ถูกต้อง', questions: ['text::1. วิธีการรวบรวมข้อมูลที่นักเรียนเลือกใช้คือวิธีใด', 'text::2. อธิบายขั้นตอนการทำงาน:'] },
                    { id: 'cs_ws5', title: 'กิจกรรมที่ 1.5 การประมวลผลข้อมูล', desc: 'วิเคราะห์การประมวลผลข้อมูลเพื่อนำไปใช้', questions: ['text::1. การประมวลผลข้อมูลมีประโยชน์อย่างไร:', 'text::2. ยกตัวอย่างการประมวลผลข้อมูลในชีวิตประจำวัน:'] },
                    { id: 'cs_ws6', title: 'กิจกรรมที่ 2.1 แนวคิดเชิงนามธรรม', desc: 'ทำความเข้าใจแนวคิดเชิงนามธรรมในการแก้ปัญหา', questions: ['text::1. แนวคิดเชิงนามธรรม (Abstraction) คืออะไร:', 'text::2. จงยกตัวอย่างสถานการณ์ที่ใช้แนวคิดนี้:'] },
                    { id: 'cs_ws7', title: 'กิจกรรมที่ 2.2 การแยกแยะปัญหา', desc: 'การแตกปัญหาย่อยเพื่อหาวิธีแก้ไข', questions: ['text::1. ปัญหาใหญ่ที่พบคืออะไร:', 'text::2. สามารถแบ่งเป็นปัญหาย่อยได้อย่างไรบ้าง:'] },
                    { id: 'cs_ws8', title: 'กิจกรรมที่ 2.3 การออกแบบขั้นตอนวิธี', desc: 'ออกแบบอัลกอริทึม (Algorithm) สำหรับแก้ปัญหา', questions: ['text::1. ให้อธิบายอัลกอริทึมการต้มบะหมี่กึ่งสำเร็จรูปเป็นข้อๆ:', 'dragdrop::2. เรียงลำดับขั้นตอนให้ถูกต้อง::ต้มน้ำให้เดือด;;ใส่บะหมี่ลงไป;;ฉีกซอง;;รอ 3 นาทีแล้วรับประทาน'] },
                    { id: 'cs_ws9', title: 'กิจกรรมที่ 3.1 รู้จักภาษา Python', desc: 'อธิบายหลักการเบื้องต้นของภาษาไพทอน', questions: ['text::1. ภาษา Python มีจุดเด่นอย่างไร:', 'radio::2. ข้อใดคือคำสั่งแสดงผลใน Python?::print();;echo();;show()'] },
                    { id: 'cs_ws10', title: 'กิจกรรมที่ 3.2 ตัวแปรและชนิดข้อมูล', desc: 'ทำความเข้าใจการประกาศตัวแปรในโปรแกรม', questions: ['text::1. ตัวแปร (Variable) มีหน้าที่ทำอะไร:', 'match::2. จับคู่ชนิดข้อมูล::int=จำนวนเต็ม;;float=ทศนิยม;;string=ข้อความ'] },
                    { id: 'cs_ws11', title: 'กิจกรรมที่ 3.3 การทำงานแบบมีเงื่อนไข (if-else)', desc: 'การเขียนโปรแกรมเพื่อตัดสินใจ', questions: ['text::1. คำสั่ง if-else ใช้ในกรณีใด:', 'text::2. จงยกตัวอย่างการใช้เงื่อนไขในชีวิตประจำวัน:'] },
                    { id: 'cs_ws12', title: 'กิจกรรมที่ 3.4 การทำงานแบบวนซ้ำ (Loop)', desc: 'การใช้คำสั่งวนซ้ำเพื่อประหยัดเวลา', questions: ['text::1. คำสั่ง for และ while ต่างกันอย่างไร:', 'text::2. ประโยชน์ของการวนซ้ำคืออะไร:'] },
                    { id: 'cs_ws13', title: 'กิจกรรมที่ 4.1 การใช้งานซอฟต์แวร์นำเสนอ', desc: 'เรียนรู้โปรแกรมสำหรับการนำเสนองาน', questions: ['checkbox::1. โปรแกรมใดใช้สำหรับนำเสนองานได้บ้าง?::Microsoft PowerPoint;;Google Slides;;Canva;;Microsoft Excel', 'text::2. ข้อดีของซอฟต์แวร์นำเสนอคืออะไร:'] },
                    { id: 'cs_ws14', title: 'กิจกรรมที่ 4.2 การสร้างกราฟและแผนภูมิ', desc: 'ใช้โปรแกรมตารางทำงาน (Spreadsheet)', questions: ['text::1. กราฟวงกลมเหมาะกับข้อมูลประเภทใด:', 'text::2. กราฟแท่งเหมาะกับข้อมูลประเภทใด:'] },
                    { id: 'cs_ws15', title: 'กิจกรรมที่ 5.1 ภัยคุกคามทางไซเบอร์', desc: 'วิเคราะห์ภัยคุกคามจากการใช้เทคโนโลยี', questions: ['text::1. ฟิชชิง (Phishing) คืออะไร และมีวิธีป้องกันอย่างไร:', 'text::2. มัลแวร์ (Malware) ส่งผลเสียต่อคอมพิวเตอร์อย่างไร:'] },
                    { id: 'cs_ws16', title: 'กิจกรรมที่ 5.2 การตั้งรหัสผ่านที่ปลอดภัย', desc: 'เรียนรู้วิธีการปกป้องข้อมูลส่วนตัว', questions: ['text::1. รหัสผ่านที่ดีควรมีลักษณะอย่างไร:', 'text::2. ให้นักเรียนลองตั้งรหัสผ่านที่ปลอดภัยมา 1 รหัส:'] },
                    { id: 'cs_ws17', title: 'กิจกรรมที่ 6.1 จริยธรรมในโลกออนไลน์', desc: 'การเป็นพลเมืองดิจิทัลที่ดี', questions: ['text::1. พลเมืองดิจิทัลที่ดีควรปฏิบัติตนอย่างไร:', 'text::2. การรังแกบนโลกไซเบอร์ (Cyberbullying) ส่งผลกระทบอย่างไร:'] },
                    { id: 'cs_ws18', title: 'กิจกรรมที่ 6.2 การประเมินความน่าเชื่อถือของข้อมูล', desc: 'รู้เท่าทันสื่อและข่าวปลอม (Fake News)', questions: ['text::1. เราจะตรวจสอบได้อย่างไรว่าข่าวสารนั้นเป็นความจริง:', 'radio::2. โดเมนเนมใดมักเป็นของหน่วยงานรัฐบาลไทย?::.go.th;;.com;;.ac.th'] },
                    { id: 'cs_ws19', title: 'กิจกรรมที่ 6.3 กฎหมายคอมพิวเตอร์เบื้องต้น', desc: 'เรียนรู้ข้อควรระวังในการใช้สื่อออนไลน์', questions: ['text::1. การนำรูปเพื่อนไปโพสต์ล้อเลียน ผิด พ.ร.บ. คอมพิวเตอร์ หรือไม่ เพราะเหตุใด:', 'text::2. การส่งอีเมลขยะ (Spam) มีความผิดอย่างไร:'] },
                    { id: 'cs_ws20', title: 'กิจกรรมที่ 6.4 สัญญาอนุญาตครีเอทีฟคอมมอนส์', desc: 'เรียนรู้เรื่องสิทธิ์การนำผลงานไปใช้ (Creative Commons)', questions: ['match::1. จับคู่สัญลักษณ์ CC ให้ถูกต้อง::BY=อ้างอิงแหล่งที่มา;;NC=ห้ามใช้เพื่อการค้า;;ND=ห้ามดัดแปลง', 'text::2. ประโยชน์ของ Creative Commons คืออะไร:'] },
                    { id: 'cs_ws21', title: 'กิจกรรมที่ 6.5 ผลกระทบของเทคโนโลยี', desc: 'วิเคราะห์ข้อดีข้อเสียของเทคโนโลยีในปัจจุบัน', questions: ['text::1. เทคโนโลยีส่งผลดีต่อชีวิตประจำวันอย่างไร:', 'text::2. เทคโนโลยีส่งผลเสียในด้านใดบ้าง จงยกตัวอย่าง:'] },
                    {
                        id: 'cs_ws22', title: 'กิจกรรมที่ 22 เรื่อง ลิขสิทธิ์และความเป็นส่วนตัว', desc: 'การวิเคราะห์การใช้งานสื่อและการละเมิดลิขสิทธิ์',
                        questions: [
                            'text::1. การสรุปเนื้อหาของผู้อื่นที่ได้อ่านมาแล้ว บอกถึงแหล่งที่มา ถือว่าสามารถทำได้โดยไม่เป็นการละเมิดลิขสิทธิ์ใช่หรือไม่ เพราะเหตุใด:',
                            'text::2. การโพสต์ข้อความ รูปภาพ และเช็คอินสถานที่ในสื่อสังคมออนไลน์ เช่น เฟซบุ๊ก นับว่าเป็นการเปิดเผยข้อมูลความเป็นส่วนตัวหรือไม่ เพราะเหตุใด:'
                        ]
                    }
                ]
            },
            {
                id: "subj_cs_m2", name: "💻 วิทยาการคำนวณ ม.2", desc: "รวมใบงานวิชาวิทยาการคำนวณ (19 ใบงาน)", worksheets: []
            },
            {
                id: "subj_cs_m3", name: "💻 วิทยาการคำนวณ ม.3", desc: "รวมใบงานวิชาวิทยาการคำนวณ (25 ใบงาน)", worksheets: []
            },
            {
                id: "subj_photo_m2", name: "📷 หลักการถ่ายภาพ ม.2/2, ม.2/3", desc: "ใบงานวิชาหลักการถ่ายภาพ (10 ใบงาน)", worksheets: []
            },
            {
                id: "subj_photo_m4", name: "📸 หลักการถ่ายภาพเบื้องต้น ม.4/2", desc: "ใบงานวิชาหลักการถ่ายภาพเบื้องต้น (10 ใบงาน)", worksheets: []
            },
            {
                id: "subj_ads_m5", name: "🎬 การถ่ายทำโฆษณา ม.5/2", desc: "ใบงานวิชาการถ่ายทำโฆษณา (10 ใบงาน)", worksheets: []
            },
            {
                id: "subj_biz_prog_m6", name: "⌨️ การเขียนโปรแกรมทางธุรกิจเบื้องต้น ม.6/2", desc: "ใบงานวิชาการเขียนโปรแกรมทางธุรกิจเบื้องต้น (10 ใบงาน)", worksheets: []
            }
        ]
    };

    function generateWorksheets(subjectId, totalCount, startIndex = 1, prefix = 'ws') {
        const subj = DEMO_DATA.subjects.find(s => s.id === subjectId);
        if (!subj) return;
        for (let i = startIndex; i <= totalCount; i++) {
            subj.worksheets.push({
                id: `${subjectId}_${prefix}${i}`,
                title: `ใบงานที่ ${i}`,
                desc: `ให้นักเรียนอ่านคำชี้แจงและตอบคำถามในใบงานที่ ${i}`,
                questions: [
                    `text::คำถามข้อที่ 1 ..............................................................`,
                    `text::คำถามข้อที่ 2 ..............................................................`
                ]
            });
        }
    }

    generateWorksheets('subj_cs_m2', 19);
    generateWorksheets('subj_cs_m3', 25);
    generateWorksheets('subj_photo_m2', 10);
    generateWorksheets('subj_photo_m4', 10);
    generateWorksheets('subj_ads_m5', 10);
    generateWorksheets('subj_biz_prog_m6', 10);

    // ==========================================
    // 🤖 ระบบ AI WORKSHEET GENERATOR (Gemini API)
    // ==========================================
    function openTeacherAdmin() {
        document.getElementById('teacher-pwd-input').value = '';
        document.getElementById('teacher-pwd-error').style.display = 'none';
        document.getElementById('teacher-password-overlay').style.display = 'flex';
    }

    function closeTeacherPassword() {
        document.getElementById('teacher-password-overlay').style.display = 'none';
    }

    function verifyTeacherPassword() {
        const pwd = document.getElementById('teacher-pwd-input').value;
        if (pwd === "1234") {
            closeTeacherPassword();
            showScreen('screen-teacher-admin');
        } else {
            document.getElementById('teacher-pwd-error').style.display = 'block';
        }
    }

    async function fetchWithRetry(url, options, maxRetries = 5) {
        let delays = [1000, 2000, 4000, 8000, 16000];
        for (let i = 0; i < maxRetries; i++) {
            try {
                const response = await fetch(url, options);
                if (!response.ok) {
                    if (response.status >= 400 && response.status < 500 && response.status !== 429) {
                         throw new Error(`Client Error: ${response.status}`);
                    }
                    throw new Error(`HTTP error! status: ${response.status}`);
                }
                return await response.json();
            } catch (err) {
                if (i === maxRetries - 1 || err.message.includes('Client Error')) throw err;
                await new Promise(resolve => setTimeout(resolve, delays[i]));
            }
        }
    }

    async function generateWorksheetWithAI() {
        const promptText = document.getElementById('ai-prompt-input').value;
        if(!promptText.trim()) { 
            showAlert('⚠️ กรุณาพิมพ์หัวข้อหรือเนื้อหาที่ต้องการให้ AI สร้างก่อนครับ', 'error'); 
            return; 
        }

        const systemPrompt = `คุณคือครูผู้เชี่ยวชาญในการสร้างใบงาน Interactive 
        จงสร้างชุดคำถามตามหัวข้อที่ผู้ใช้สั่ง โดยบังคับใช้รูปแบบ Syntax ด้านล่างนี้เท่านั้น และคั่นแต่ละข้อด้วยเครื่องหมาย | 
        (ห้ามมีข้อความอธิบายทักทายหรือ Markdown ใดๆ ทั้งสิ้น ให้ตอบกลับมาเป็นโค้ดบรรทัดเดียว)

        รูปแบบที่อนุญาต:
        1. พิมพ์ตอบ -> text::[คำถาม]
        2. เลือกข้อเดียว -> radio::[คำถาม]::[ตัวเลือก1];;[ตัวเลือก2];;[ตัวเลือก3]
        3. เลือกหลายข้อ -> checkbox::[คำถาม]::[ตัวเลือก1];;[ตัวเลือก2];;[ตัวเลือก3]
        4. จับคู่ -> match::[คำถาม]::[โจทย์1]=[คำตอบ1];;[โจทย์2]=[คำตอบ2]
        5. เรียงลำดับ -> dragdrop::[คำถาม]::[คำที่1];;[คำที่2];;[คำที่3]
        6. วาดรูป -> draw::[คำสั่งให้วาด]
        7. อัดเสียง -> voice::[คำสั่งให้อ่าน]

        ตัวอย่างผลลัพธ์ที่คุณต้องสร้าง:
        text::1. อธิบายความหมายของ AI | radio::2. ข้อใดคือ AI?::หุ่นยนต์;;พัดลม | match::3. จับคู่::AI=ปัญญาประดิษฐ์;;IoT=อินเทอร์เน็ตในทุกสิ่ง | draw::4. วาดรูปหุ่นยนต์`;

        const btn = document.getElementById('generate-ai-btn');
        const originalText = btn.innerHTML;
        btn.innerHTML = '⏳ กำลังให้ AI ประมวลผลและแต่งข้อสอบ...';
        btn.disabled = true;

        // ระบบจะลองใช้โมเดลสำหรับหน้าต่าง Preview ก่อน
        let url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;
        
        try {
            let result;
            try {
                // พยายามเรียกโมเดล 2.5 Preview
                result = await fetchWithRetry(url, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: promptText }] }],
                        systemInstruction: { parts: [{ text: systemPrompt }] }
                    })
                });
            } catch (firstErr) {
                // หากเจอ Error 404 (แสดงว่าคุณครูใช้ API Key ของตนเองนอกระบบ Canvas) 
                // ให้ทำการสลับไปใช้รุ่นมาตรฐาน (1.5-flash) อัตโนมัติทันที
                if (firstErr.message.includes('404')) {
                    console.log("Switching to gemini-1.5-flash fallback...");
                    url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${apiKey}`;
                    result = await fetchWithRetry(url, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify({
                            contents: [{ parts: [{ text: promptText }] }],
                            systemInstruction: { parts: [{ text: systemPrompt }] }
                        })
                    });
                } else {
                    throw firstErr; // โยน Error อื่นๆ ออกไปให้ catch ด้านล่างจัดการ
                }
            }
            
            const aiText = result.candidates?.[0]?.content?.parts?.[0]?.text || '';
            document.getElementById('ai-output-result').value = aiText.trim();
            showAlert('✨ AI สร้างคำถามเสร็จเรียบร้อย!', 'success');
        } catch(err) {
            console.error(err);
            if (apiKey === "") {
                showAlert('❌ ระบบ AI ไม่สามารถทำงานได้<br><br>(คุณครูต้องไปรับ API Key ฟรีจาก Google แล้วนำมาใส่ในโค้ดบรรทัด 468 ก่อนครับ)', 'error');
            } else {
                showAlert('❌ เกิดข้อผิดพลาดในการเชื่อมต่อ AI: ' + err.message, 'error');
            }
        } finally {
            btn.innerHTML = originalText;
            btn.disabled = false;
        }
    }

    function copyAIOutput() {
        const copyText = document.getElementById("ai-output-result");
        if(!copyText.value) return;
        copyText.select();
        copyText.setSelectionRange(0, 99999); 
        document.execCommand("copy");
        showAlert('📋 คัดลอกข้อความเรียบร้อยแล้ว! นำไปวางใน Google Sheets ได้เลย', 'success');
    }

    // ==========================================
    // 🔔 ระบบกล่องแจ้งเตือนและการยืนยัน
    // ==========================================
    function showAlert(message, type="error") {
        const titleEl = document.getElementById('custom-alert-title');
        const boxEl = document.getElementById('custom-alert-box');
        const btnEl = document.getElementById('custom-alert-btn');
        titleEl.innerHTML = message;
        if (type === 'success') {
            boxEl.style.borderColor = '#2ecc71'; titleEl.style.color = '#2ecc71';
            btnEl.style.borderColor = '#2ecc71'; btnEl.style.color = '#2ecc71';
        } else {
            boxEl.style.borderColor = '#e74c3c'; titleEl.style.color = '#e74c3c';
            btnEl.style.borderColor = '#e74c3c'; btnEl.style.color = '#e74c3c';
        }
        document.getElementById('custom-alert-overlay').style.display = 'flex';
    }
    function closeCustomAlert() { document.getElementById('custom-alert-overlay').style.display = 'none'; }
    function showCustomAlert() { showAlert("⚠️ กรุณาตอบคำถามให้ครบทุกข้อ (รวมถึงการบันทึกเสียงและวาดรูป)", "error"); }

    let confirmCallback = null;
    function showCustomConfirm(title, message, callback) {
        document.getElementById('confirm-title').innerHTML = title;
        document.getElementById('confirm-message').innerHTML = message;
        confirmCallback = callback;
        document.getElementById('custom-confirm-overlay').style.display = 'flex';
    }
    function closeCustomConfirm() { document.getElementById('custom-confirm-overlay').style.display = 'none'; confirmCallback = null; }
    function executeConfirm() { if (confirmCallback) confirmCallback(); closeCustomConfirm(); }

    // ==========================================
    // 🧠 ระบบการทำงานหลัก และ Parsing
    // ==========================================
    const DB_KEY = 'school_portal_progress_db'; 
    let currentUser = null;
    let currentSubjectId = null; 
    let progressDB = JSON.parse(localStorage.getItem(DB_KEY)) || {};
    let audioStreams = {}; 

    function showScreen(screenId) {
        document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
        document.getElementById(screenId).classList.add('active');
        window.scrollTo(0, 0);
    }

    function sanitizeAllSubjects() {
        allSubjects.forEach(subj => {
            if(subj.worksheets) {
                subj.worksheets.forEach(ws => {
                    let processed = [];
                    ws.questions.forEach(q => {
                        let subQs = String(q).split(/\n|\|/);
                        subQs.forEach(sq => { if(sq.trim()) processed.push(sq.trim()); });
                    });
                    ws.questions = processed;
                });
            }
        });
    }

    async function fetchGoogleSheetsData() {
        if (!GOOGLE_SHEET_API_URL) {
            studentDB = DEMO_DATA.students;
            allSubjects = DEMO_DATA.subjects;
            sanitizeAllSubjects();
            setTimeout(() => { renderSubjects(); }, 1000);
            return;
        }
        try {
            const response = await fetch(GOOGLE_SHEET_API_URL);
            const data = await response.json();
            studentDB = data.students || {};
            allSubjects = data.subjects || [];
            sanitizeAllSubjects();
            renderSubjects();
        } catch (error) {
            showAlert("❌ ไม่สามารถดึงข้อมูลจาก Google Sheets ได้", "error");
        }
    }

    function parseQuestionData(qStr) {
        if (typeof qStr !== 'string') return { type: 'text', text: String(qStr) };
        qStr = qStr.trim();
        let type = 'text'; let text = qStr; let options = [];
        const knownTypes = ['text', 'dropdown', 'radio', 'checkbox', 'match', 'dragdrop', 'draw', 'voice', 'media-yt', 'media-img', 'media-vid', 'media-aud'];
        
        let separator = qStr.includes('::') ? '::' : (qStr.includes(':') ? ':' : null);
        
        if (separator) {
            let parts = qStr.split(separator);
            let potentialType = parts[0].trim().toLowerCase(); 
            
            if (knownTypes.includes(potentialType)) {
                type = potentialType;
                text = parts[1] ? parts[1].trim() : '';
                
                if (parts.length > 2) {
                    let optsStr = parts.slice(2).join(separator);
                    if (optsStr.includes(';;')) options = optsStr.split(';;');
                    else if (optsStr.includes('//')) options = optsStr.split('//');
                    else if (optsStr.includes(';')) options = optsStr.split(';');
                    else options = optsStr.split(',');
                    options = options.map(s => s.trim()).filter(s => s !== '');
                }
            }
        }
        return { type, text, options };
    }

    function renderSubjects() {
        const container = document.getElementById('subjects-container');
        let html = '';
        allSubjects.forEach(subj => {
            html += `
                <div class="card subject-card" style="cursor: pointer;" onclick="selectSubjectForLogin('${subj.id}')">
                    <div class="card-info">
                        <h3 style="color: var(--accent); font-size: 20px;">${subj.name}</h3>
                        <p>${subj.desc}</p>
                    </div>
                    <div class="card-footer" style="justify-content: flex-end;">
                        <span style="font-weight: bold; color: #7f8c8d;">มี ${subj.worksheets ? subj.worksheets.length : 0} ใบงาน ➡️</span>
                    </div>
                </div>
            `;
        });
        container.innerHTML = html;
        showScreen('screen-subjects');
    }

    function selectSubjectForLogin(subjId) {
        currentSubjectId = subjId;
        const subj = allSubjects.find(s => s.id === subjId);
        document.getElementById('login-subject-title').innerText = `เข้าสู่ระบบ: ${subj.name}`;
        ['login-id', 'login-name', 'login-class', 'login-roll'].forEach(id => document.getElementById(id).value = '');
        showScreen('screen-login');
    }

    function checkStudentId() {
        const id = document.getElementById('login-id').value.trim();
        if (studentDB[id]) {
            document.getElementById('login-name').value = studentDB[id].name;
            document.getElementById('login-class').value = studentDB[id].class;
            document.getElementById('login-roll').value = studentDB[id].roll;
        } else {
            document.getElementById('login-name').value = '';
            document.getElementById('login-class').value = '';
            document.getElementById('login-roll').value = '';
        }
    }

    function handleLogin() {
        const id = document.getElementById('login-id').value.trim();
        const name = document.getElementById('login-name').value.trim();
        if (!id) { showAlert('⚠️ กรุณากรอกรหัสประจำตัวนักเรียน'); return; }
        if (!studentDB[id] || !name) { showAlert('⚠️ ไม่พบข้อมูลรหัสนักเรียนในระบบ'); return; }

        currentUser = progressDB[id] || { id, name, class: document.getElementById('login-class').value, roll: document.getElementById('login-roll').value, progress: {} };
        saveProgressToLocal();
        updateUserBar();
        openSubjectDashboard(currentSubjectId); 
    }

    function handleLogout() {
        currentUser = null;
        currentSubjectId = null;
        document.getElementById('user-bar').style.display = 'none';
        renderSubjects(); 
    }

    function updateUserBar() {
        document.getElementById('user-bar').style.display = 'flex';
        document.getElementById('display-user-info').innerText = `👤 ${currentUser.name} (${currentUser.class} เลขที่ ${currentUser.roll})`;
    }

    function saveProgressToLocal() {
        if (currentUser) {
            progressDB[currentUser.id] = currentUser;
            localStorage.setItem(DB_KEY, JSON.stringify(progressDB));
        }
    }

    function openSubjectDashboard(subjId) {
        currentSubjectId = subjId;
        const subj = allSubjects.find(s => s.id === subjId);
        document.getElementById('dashboard-subject-title').innerText = subj.name;
        const container = document.getElementById('dashboard-container');
        let html = '';
        if(subj.worksheets) {
            subj.worksheets.forEach((ws) => {
                const isCompleted = currentUser.progress[ws.id] && currentUser.progress[ws.id].completed;
                html += `
                    <div class="card">
                        <div class="card-info">
                            <h3>${ws.title}</h3>
                            <p>${ws.desc || ''}</p>
                        </div>
                        <div class="card-footer">
                            <span class="status-badge ${isCompleted ? 'status-complete' : 'status-incomplete'}">${isCompleted ? '✔️ ทำเสร็จแล้ว' : 'ยังไม่ทำ'}</span>
                            <button class="btn btn-outline" style="width: auto; padding: 8px 15px;" onclick="openWorksheet('${ws.id}')">📝 เข้าทำใบงาน</button>
                        </div>
                    </div>
                `;
            });
        }
        container.innerHTML = html;
        showScreen('screen-dashboard');
    }

    // ==========================================
    // 🎨 RENDERER: สร้างฟอร์มตามรูปแบบ
    // ==========================================
    function openWorksheet(wsId) {
        const subj = allSubjects.find(s => s.id === currentSubjectId);
        const ws = subj.worksheets.find(w => w.id === wsId);
        const progress = currentUser.progress[wsId] || {};
        
        let html = `
            <div id="worksheet-capture-area" style="background: #fff; padding-bottom: 20px;">
                <div class="header" style="border-radius: 8px 8px 0 0;">
                    <p style="margin:0; font-size: 14px; opacity:0.8;">วิชา: ${subj.name}</p>
                    <h1 style="margin-top: 5px;">${ws.title}</h1>
                    <p style="margin-top: 15px; font-size: 15px; background: rgba(255,255,255,0.2); display: inline-block; padding: 6px 15px; border-radius: 20px;">
                        👤 ${currentUser.name} | ชั้น ${currentUser.class} | เลขที่ ${currentUser.roll}
                    </p>
                </div>
                <div class="content" style="padding: 20px;">
                    <p style="font-size:18px; color:#555; margin-bottom: 25px;">${ws.desc || ''}</p>
        `;
        
        let canvasIds = [];
        
        ws.questions.forEach((rawQ, index) => {
            const q = parseQuestionData(rawQ);
            const ans = (progress.answers && progress.answers[index]) ? progress.answers[index] : null;
            
            html += `<div class="form-group" data-qtype="${q.type}" id="q-container-${index}">`;
            
            if (q.type.startsWith('media-')) {
                if (q.type === 'media-yt') {
                    html += `<div class="media-container"><iframe src="${q.text}" allowfullscreen></iframe></div>`;
                } else if (q.type === 'media-img') {
                    html += `<div class="media-container"><img src="${q.text}" alt="Image"></div>`;
                } else if (q.type === 'media-vid') {
                    html += `<div class="media-container"><video src="${q.text}" controls></video></div>`;
                } else if (q.type === 'media-aud') {
                    html += `<div class="media-audio"><audio src="${q.text}" controls></audio></div>`;
                }
            } 
            else {
                html += `<label>${q.text}</label>`;
                
                if (q.type === 'text') {
                    html += `<textarea id="ans-${index}" rows="3" placeholder="พิมพ์คำตอบที่นี่...">${ans || ''}</textarea>`;
                } 
                else if (q.type === 'dropdown') {
                    html += `<select id="ans-${index}">`;
                    html += `<option value="">-- โปรดเลือก --</option>`;
                    q.options.forEach(opt => {
                        let selected = (ans === opt) ? 'selected' : '';
                        html += `<option value="${opt}" ${selected}>${opt}</option>`;
                    });
                    html += `</select>`;
                }
                else if (q.type === 'radio') {
                    html += `<div class="radio-group">`;
                    q.options.forEach((opt, i) => {
                        let checked = (ans === opt) ? 'checked' : '';
                        html += `<label><input type="radio" name="ans-${index}" value="${opt}" ${checked}> ${opt}</label>`;
                    });
                    html += `</div>`;
                }
                else if (q.type === 'checkbox') {
                    let ansArray = ans ? ans.split(',') : [];
                    html += `<div class="checkbox-group">`;
                    q.options.forEach((opt, i) => {
                        let checked = ansArray.includes(opt) ? 'checked' : '';
                        html += `<label><input type="checkbox" name="ans-${index}" value="${opt}" ${checked}> ${opt}</label>`;
                    });
                    html += `</div>`;
                }
                else if (q.type === 'match') {
                    html += `<div id="match-container-${index}">`;
                    let rightOptions = q.options.map(pair => pair.split('=')[1]);
                    rightOptions.sort(() => Math.random() - 0.5); 
                    
                    q.options.forEach((pair, i) => {
                        let [left, right] = pair.split('=');
                        let savedMatch = (ans && ans[`match_${i}`]) ? ans[`match_${i}`] : '';
                        
                        html += `<div class="match-row">
                                    <div class="match-left">${left}</div>
                                    <div class="match-right">
                                        <select id="ans-${index}-match-${i}">
                                            <option value="">-- เลือกจับคู่ --</option>`;
                        rightOptions.forEach(opt => {
                            let selected = (savedMatch === opt) ? 'selected' : '';
                            html += `<option value="${opt}" ${selected}>${opt}</option>`;
                        });
                        html += `       </select>
                                    </div>
                                 </div>`;
                    });
                    html += `</div>`;
                }
                else if (q.type === 'dragdrop') {
                    let items = ans ? ans.split(';;') : q.options;
                    html += `<ul id="sort-${index}" class="sort-list">`;
                    items.forEach((opt, i) => {
                        html += `<li>
                                    <span class="sort-text">${opt}</span> 
                                    <div class="sort-btn-group">
                                        <button type="button" onclick="moveItemUp(this)">⬆️</button>
                                        <button type="button" onclick="moveItemDown(this)">⬇️</button>
                                    </div>
                                 </li>`;
                    });
                    html += `</ul>`;
                }
                else if (q.type === 'voice') {
                    html += `<button type="button" class="voice-record-btn" id="voice-btn-${index}" onclick="toggleRecord(${index})">🎙️ เริ่มบันทึกเสียง</button>
                             <audio id="voice-audio-${index}" controls style="display: ${ans ? 'block' : 'none'}; width:100%; margin-top: 10px;" src="${ans || ''}"></audio>
                             <input type="hidden" id="ans-${index}" value="${ans || ''}">`;
                }
                else if (q.type === 'draw') {
                    html += `
                        <div class="canvas-tools">
                            <button type="button" class="btn btn-outline btn-small" onclick="clearCanvas('canvas-${index}')">🗑️ ลบภาพวาด</button>
                        </div>
                        <div class="canvas-container">
                            <canvas id="canvas-${index}"></canvas>
                        </div>
                        <input type="hidden" id="ans-${index}" value="${ans || ''}">`;
                    canvasIds.push(`canvas-${index}`);
                }
            }
            html += `</div>`;
        });
        
        html += `
                </div>
            </div>
            <div class="button-group">
                <button class="btn btn-outline" onclick="openSubjectDashboard('${subj.id}')">⬅️ ย้อนกลับ</button>
                <button class="btn btn-success" onclick="saveWorksheet('${ws.id}')">💾 บันทึกส่งงาน</button>
                <button id="btn-capture" class="btn btn-capture" onclick="saveAsImage('${ws.id}')">📸 บันทึกเป็นรูปภาพ</button>
            </div>
        `;
        
        document.getElementById('screen-worksheet').innerHTML = html;
        showScreen('screen-worksheet');
        
        setTimeout(() => {
            canvasIds.forEach(id => {
                initCanvas(id);
                let savedData = document.getElementById(id.replace('canvas-', 'ans-')).value;
                if(savedData) loadCanvasImage(id, savedData);
            });
        }, 50);
    }

    // ==========================================
    // 🕹️ INTERACTIVE LOGIC (Sort, Record, Draw)
    // ==========================================
    function moveItemUp(btn) {
        let li = btn.closest('li');
        if(li.previousElementSibling) li.parentNode.insertBefore(li, li.previousElementSibling);
    }
    function moveItemDown(btn) {
        let li = btn.closest('li');
        if(li.nextElementSibling) li.parentNode.insertBefore(li.nextElementSibling, li);
    }

    let mediaRecorders = {};
    let audioChunks = {};
    async function toggleRecord(index) {
        const btn = document.getElementById(`voice-btn-${index}`);
        const audioEl = document.getElementById(`voice-audio-${index}`);
        const inputEl = document.getElementById(`ans-${index}`);

        if (mediaRecorders[index] && mediaRecorders[index].state === 'recording') {
            mediaRecorders[index].stop();
            btn.innerHTML = '🎙️ บันทึกเสียงใหม่';
            btn.classList.remove('recording');
        } else {
            try {
                const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
                mediaRecorders[index] = new MediaRecorder(stream);
                audioChunks[index] = [];
                mediaRecorders[index].ondataavailable = e => audioChunks[index].push(e.data);
                mediaRecorders[index].onstop = () => {
                    const blob = new Blob(audioChunks[index], { type: 'audio/webm' });
                    const reader = new FileReader();
                    reader.onloadend = () => {
                        inputEl.value = reader.result; 
                        audioEl.src = reader.result;
                        audioEl.style.display = 'block';
                    };
                    reader.readAsDataURL(blob);
                };
                mediaRecorders[index].start();
                btn.innerHTML = '⏹️ กำลังบันทึก (กดเพื่อหยุด)';
                btn.classList.add('recording');
            } catch (err) {
                showAlert('❌ ไม่สามารถเข้าถึงไมโครโฟนได้ กรุณาอนุญาตให้ใช้งานไมค์', 'error');
            }
        }
    }

    let ctxMap = {};
    function initCanvas(canvasId) {
        const canvas = document.getElementById(canvasId);
        const ctx = canvas.getContext('2d');
        ctxMap[canvasId] = ctx;
        canvas.width = canvas.parentElement.clientWidth;
        canvas.height = 300; 
        ctx.fillStyle = "white"; ctx.fillRect(0, 0, canvas.width, canvas.height);
        
        let isDrawing = false;
        function getPos(e) {
            const rect = canvas.getBoundingClientRect();
            let cX = e.clientX, cY = e.clientY;
            if (e.touches && e.touches.length > 0) { cX = e.touches[0].clientX; cY = e.touches[0].clientY; }
            return { x: cX - rect.left, y: cY - rect.top };
        }
        function start(e) { isDrawing = true; draw(e); }
        function stop() { isDrawing = false; ctx.beginPath(); document.getElementById(canvasId.replace('canvas-','ans-')).value = canvas.toDataURL(); }
        function draw(e) {
            if (!isDrawing) return; e.preventDefault(); 
            const pos = getPos(e);
            ctx.lineWidth = 3; ctx.lineCap = 'round'; ctx.strokeStyle = '#2c3e50';
            ctx.lineTo(pos.x, pos.y); ctx.stroke();
            ctx.beginPath(); ctx.moveTo(pos.x, pos.y);
        }
        canvas.addEventListener('mousedown', start); canvas.addEventListener('mousemove', draw);
        canvas.addEventListener('mouseup', stop); canvas.addEventListener('mouseout', stop);
        canvas.addEventListener('touchstart', start, {passive: false}); canvas.addEventListener('touchmove', draw, {passive: false});
        canvas.addEventListener('touchend', stop);
    }
    function clearCanvas(canvasId) {
        showCustomConfirm("🗑️ ยืนยันการลบ", "ต้องการลบภาพวาดใช่หรือไม่?", function() {
            const canvas = document.getElementById(canvasId);
            ctxMap[canvasId].fillStyle = "white";
            ctxMap[canvasId].fillRect(0, 0, canvas.width, canvas.height);
            document.getElementById(canvasId.replace('canvas-','ans-')).value = '';
        });
    }
    function loadCanvasImage(canvasId, dataUrl) {
        const img = new Image();
        img.onload = function() { ctxMap[canvasId].drawImage(img, 0, 0); };
        img.src = dataUrl;
    }

    // ==========================================
    // 💾 SAVE & EXTRACT DATA
    // ==========================================
    function getAnswersFromDOM(wsId) {
        const subj = allSubjects.find(s => s.id === currentSubjectId);
        const ws = subj.worksheets.find(w => w.id === wsId);
        let answers = [];
        let isComplete = true;

        ws.questions.forEach((rawQ, index) => {
            const q = parseQuestionData(rawQ);
            if (q.type.startsWith('media-')) {
                answers.push(null); 
                return;
            }

            let val = '';
            if (q.type === 'text' || q.type === 'dropdown' || q.type === 'voice' || q.type === 'draw') {
                val = document.getElementById(`ans-${index}`).value;
                if (!val || val.trim() === '') isComplete = false;
            } 
            else if (q.type === 'radio') {
                const checked = document.querySelector(`input[name="ans-${index}"]:checked`);
                val = checked ? checked.value : '';
                if (!val) isComplete = false;
            } 
            else if (q.type === 'checkbox') {
                const checkeds = Array.from(document.querySelectorAll(`input[name="ans-${index}"]:checked`));
                val = checkeds.map(el => el.value).join(',');
                if (val === '') isComplete = false;
            }
            else if (q.type === 'match') {
                val = {};
                q.options.forEach((p, i) => {
                    let mVal = document.getElementById(`ans-${index}-match-${i}`).value;
                    if (!mVal) isComplete = false;
                    val[`match_${i}`] = mVal;
                });
            }
            else if (q.type === 'dragdrop') {
                const listItems = document.querySelectorAll(`#sort-${index} .sort-text`);
                val = Array.from(listItems).map(el => el.innerText).join(';;');
            }
            answers.push(val);
        });
        return { answers, isComplete };
    }

    function saveWorksheet(wsId) {
        const result = getAnswersFromDOM(wsId);
        if (!result.isComplete) { showCustomAlert(); return; }

        currentUser.progress[wsId] = { completed: true, answers: result.answers };
        saveProgressToLocal();
        showAlert('✔️ บันทึกข้อมูลใบงานสำเร็จแล้ว!', 'success');
        openSubjectDashboard(currentSubjectId); 
    }

    // ==========================================
    // 📸 CAPTURE IMAGE
    // ==========================================
    function saveAsImage(wsId) {
        const result = getAnswersFromDOM(wsId);
        if (!result.isComplete) { showCustomAlert(); return; }

        currentUser.progress[wsId] = { completed: true, answers: result.answers };
        saveProgressToLocal();

        const subj = allSubjects.find(s => s.id === currentSubjectId);
        const ws = subj.worksheets.find(w => w.id === wsId);
        
        ws.questions.forEach((rawQ, index) => {
            const q = parseQuestionData(rawQ);
            if (q.type === 'text') {
                const txt = document.getElementById(`ans-${index}`);
                txt.innerHTML = txt.value; 
            } else if (q.type === 'dropdown' || q.type === 'match') {
                const selects = document.querySelectorAll(`#q-container-${index} select`);
                selects.forEach(sel => {
                    Array.from(sel.options).forEach(opt => {
                        if(opt.value === sel.value) opt.setAttribute('selected', 'selected');
                        else opt.removeAttribute('selected');
                    });
                });
            } else if (q.type === 'radio' || q.type === 'checkbox') {
                const inputs = document.querySelectorAll(`#q-container-${index} input`);
                inputs.forEach(inp => {
                    if(inp.checked) inp.setAttribute('checked', 'checked');
                    else inp.removeAttribute('checked');
                });
            }
        });

        const container = document.getElementById('worksheet-capture-area');
        const captureBtn = document.getElementById('btn-capture');
        const originalText = captureBtn.innerHTML;
        captureBtn.innerHTML = '⏳ กำลังประมวลผลภาพ...';
        
        window.scrollTo({ top: 0, behavior: 'instant' });

        setTimeout(() => {
            html2canvas(container, { scale: 2, useCORS: true, backgroundColor: '#ffffff' }).then(canvas => {
                let safeName = currentUser.name.replace(/[\\/:*?"<>|]/g, '');
                let fileName = `ใบงาน_${subj.name}_${ws.title}_${safeName}.png`;
                
                let link = document.createElement('a');
                link.download = fileName;
                link.href = canvas.toDataURL('image/png');
                link.click();
                
                captureBtn.innerHTML = originalText;
                showAlert('📸 บันทึกรูปภาพสำเร็จ!', 'success');
            }).catch(err => {
                showAlert("เกิดข้อผิดพลาดในการบันทึกภาพ: " + err, 'error');
                captureBtn.innerHTML = originalText;
            });
        }, 300);
    }

    window.onload = function() {
        fetchGoogleSheetsData();
    };
</script>
</body>
</html>
