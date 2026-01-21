<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบรายงานความเสี่ยง (Risk Management System)</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;500;600&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Sarabun', sans-serif;
            background-color: #f8fafc;
        }
        .risk-option:checked + label {
            transform: scale(1.05);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
            border-color: currentColor;
        }
        /* สำหรับตกแต่งส่วน iframe */
        .iframe-wrapper {
            position: relative;
            padding-bottom: 56.25%; /* 16:9 Aspect Ratio */
            height: 0;
            overflow: hidden;
        }
        .iframe-wrapper iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }
    </style>
</head>
<body class="text-slate-900">

    <!-- Header Section -->
    <header class="bg-white border-b border-slate-200 sticky top-0 z-40">
        <div class="max-w-4xl mx-auto px-4 py-4 flex items-center justify-between">
            <div class="flex items-center gap-3">
                <div class="bg-red-600 p-2 rounded-lg">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
                    </svg>
                </div>
                <h1 class="text-xl font-bold text-slate-800">ระบบรายงานความเสี่ยง</h1>
            </div>
            <span class="text-xs font-medium px-2 py-1 bg-slate-100 text-slate-500 rounded">v1.0.2</span>
        </div>
    </header>

    <main class="max-w-4xl mx-auto px-4 py-8 space-y-8">
        
        <!-- Form Container -->
        <div class="bg-white rounded-2xl shadow-xl shadow-slate-200/60 border border-slate-100 overflow-hidden">
            <div class="p-6 sm:p-8">
                <h2 class="text-lg font-semibold mb-6 flex items-center gap-2 text-slate-700">
                    <span class="w-1.5 h-6 bg-blue-600 rounded-full"></span>
                    กรอกข้อมูลรายงานอุบัติการณ์
                </h2>

                <form id="riskForm" class="space-y-6">
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <!-- 1. Date -->
                        <div class="space-y-1.5">
                            <label for="incidentDate" class="text-sm font-semibold text-slate-700">1. วัน/เดือน/ปี ที่เกิดเหตุ <span class="text-red-500">*</span></label>
                            <input type="datetime-local" id="incidentDate" name="date" required 
                                class="w-full p-3 rounded-xl border border-slate-200 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all outline-none">
                        </div>

                        <!-- 2. Department -->
                        <div class="space-y-1.5">
                            <label for="department" class="text-sm font-semibold text-slate-700">2. หน่วยงาน/แผนกที่เกี่ยวข้อง <span class="text-red-500">*</span></label>
                            <input type="text" id="department" name="department" required placeholder="พิมพ์ระบุชื่อหน่วยงาน..."
                                class="w-full p-3 rounded-xl border border-slate-200 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all outline-none">
                        </div>
                    </div>

                    <!-- 3. Risk Level -->
                    <div class="space-y-3">
                        <label class="text-sm font-semibold text-slate-700">3. ให้คะแนนระดับความเสี่ยง (1-5) <span class="text-red-500">*</span></label>
                        <div class="grid grid-cols-5 gap-3">
                            <div class="relative">
                                <input type="radio" name="riskLevel" id="r1" value="1" class="peer sr-only risk-option" required>
                                <label for="r1" class="flex flex-col items-center justify-center p-3 rounded-xl border-2 border-slate-100 bg-slate-50 cursor-pointer hover:bg-green-50 peer-checked:bg-green-600 peer-checked:border-green-600 peer-checked:text-white transition-all">
                                    <span class="text-lg font-bold">1</span>
                                    <span class="text-[10px]">ต่ำมาก</span>
                                </label>
                            </div>
                            <div class="relative">
                                <input type="radio" name="riskLevel" id="r2" value="2" class="peer sr-only risk-option">
                                <label for="r2" class="flex flex-col items-center justify-center p-3 rounded-xl border-2 border-slate-100 bg-slate-50 cursor-pointer hover:bg-lime-50 peer-checked:bg-lime-500 peer-checked:border-lime-500 peer-checked:text-white transition-all">
                                    <span class="text-lg font-bold">2</span>
                                    <span class="text-[10px]">ต่ำ</span>
                                </label>
                            </div>
                            <div class="relative">
                                <input type="radio" name="riskLevel" id="r3" value="3" class="peer sr-only risk-option">
                                <label for="r3" class="flex flex-col items-center justify-center p-3 rounded-xl border-2 border-slate-100 bg-slate-50 cursor-pointer hover:bg-yellow-50 peer-checked:bg-yellow-500 peer-checked:border-yellow-500 peer-checked:text-white transition-all">
                                    <span class="text-lg font-bold">3</span>
                                    <span class="text-[10px]">ปานกลาง</span>
                                </label>
                            </div>
                            <div class="relative">
                                <input type="radio" name="riskLevel" id="r4" value="4" class="peer sr-only risk-option">
                                <label for="r4" class="flex flex-col items-center justify-center p-3 rounded-xl border-2 border-slate-100 bg-slate-50 cursor-pointer hover:bg-orange-50 peer-checked:bg-orange-500 peer-checked:border-orange-500 peer-checked:text-white transition-all">
                                    <span class="text-lg font-bold">4</span>
                                    <span class="text-[10px]">สูง</span>
                                </label>
                            </div>
                            <div class="relative">
                                <input type="radio" name="riskLevel" id="r5" value="5" class="peer sr-only risk-option">
                                <label for="r5" class="flex flex-col items-center justify-center p-3 rounded-xl border-2 border-slate-100 bg-slate-50 cursor-pointer hover:bg-red-50 peer-checked:bg-red-600 peer-checked:border-red-600 peer-checked:text-white transition-all">
                                    <span class="text-lg font-bold">5</span>
                                    <span class="text-[10px]">สูงมาก</span>
                                </label>
                            </div>
                        </div>
                    </div>

                    <!-- 4. Details -->
                    <div class="space-y-1.5">
                        <label for="details" class="text-sm font-semibold text-slate-700">4. รายละเอียด/คำบรรยายเหตุการณ์ <span class="text-red-500">*</span></label>
                        <textarea id="details" name="details" rows="4" required placeholder="เล่ารายละเอียดเหตุการณ์ที่เกิดขึ้นโดยสังเขป..."
                            class="w-full p-3 rounded-xl border border-slate-200 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all outline-none resize-none"></textarea>
                    </div>

                    <!-- 5. File Upload -->
                    <div class="space-y-1.5">
                        <label class="text-sm font-semibold text-slate-700">5. อัปโหลดไฟล์หลักฐาน (PDF/JPG/PNG) <span class="text-red-500">*</span></label>
                        <div id="dropzone" class="relative group border-2 border-dashed border-slate-200 rounded-2xl p-8 transition-all hover:bg-slate-50 hover:border-blue-400 text-center">
                            <input type="file" id="fileUpload" required accept=".pdf, .jpg, .jpeg, .png" class="absolute inset-0 w-full h-full opacity-0 cursor-pointer">
                            <div class="space-y-2">
                                <div class="bg-blue-50 w-12 h-12 rounded-full flex items-center justify-center mx-auto text-blue-600 group-hover:scale-110 transition-transform">
                                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12" />
                                    </svg>
                                </div>
                                <div class="text-slate-600">คลิกเพื่อเลือกไฟล์ หรือลากไฟล์มาวาง</div>
                                <div class="text-xs text-slate-400">รองรับ PDF, JPG และ PNG (สูงสุด 10MB)</div>
                                <div id="fileName" class="text-sm font-bold text-blue-600 mt-3 hidden"></div>
                            </div>
                        </div>
                    </div>

                    <!-- Submit -->
                    <div class="pt-4">
                        <button type="submit" id="submitBtn" class="w-full bg-slate-900 text-white font-bold py-4 rounded-xl shadow-lg shadow-slate-200 hover:bg-blue-700 hover:shadow-blue-200 transition-all active:scale-[0.98]">
                            บันทึกข้อมูลรายงาน
                        </button>
                    </div>
                </form>
            </div>
        </div>

        <!-- 6. Google Sheet Display -->
        <div class="space-y-4">
            <div class="flex items-center justify-between">
                <h2 class="text-lg font-bold text-slate-800 flex items-center gap-2">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-green-600" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M3 4a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm0 4a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm0 4a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm0 4a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z" clip-rule="evenodd" />
                    </svg>
                    6. ตารางข้อมูลความเสี่ยงผ่าน Google Sheet
                </h2>
                <a href="https://docs.google.com/spreadsheets/d/e/2PACX-1vQSAP7f-jszrwYqRfK6_DbQzpxQ902Fl86rch-Y5FwvA_7_JkhC-0cPpuCv4RBjlw/pubhtml?gid=320747993" target="_blank" class="text-sm text-blue-600 hover:underline">ขยายเต็มหน้า</a>
            </div>
            
            <div class="bg-white p-2 rounded-2xl shadow-md border border-slate-100 overflow-hidden">
                <div class="iframe-wrapper rounded-xl overflow-hidden border border-slate-50">
                    <iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vQSAP7f-jszrwYqRfK6_DbQzpxQ902Fl86rch-Y5FwvA_7_JkhC-0cPpuCv4RBjlw/pubhtml?gid=320747993&amp;single=true&amp;widget=true&amp;headers=false"></iframe>
                </div>
            </div>
        </div>

    </main>

    <!-- Success Toast -->
    <div id="toast" class="fixed bottom-6 right-6 translate-y-24 opacity-0 transition-all duration-500 pointer-events-none">
        <div class="bg-green-600 text-white px-6 py-4 rounded-2xl shadow-2xl flex items-center gap-3">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
            </svg>
            <div>
                <p class="font-bold">บันทึกสำเร็จ!</p>
                <p class="text-xs opacity-90">ข้อมูลของคุณถูกจำลองการส่งเรียบร้อยแล้ว</p>
            </div>
        </div>
    </div>

    <script>
        // Set Default Date to Now
        const dateInput = document.getElementById('incidentDate');
        const now = new Date();
        now.setMinutes(now.getMinutes() - now.getTimezoneOffset());
        dateInput.value = now.toISOString().slice(0, 16);

        // File Selection Feedback
        const fileInput = document.getElementById('fileUpload');
        const fileNameDisplay = document.getElementById('fileName');
        const dropzone = document.getElementById('dropzone');

        fileInput.addEventListener('change', (e) => {
            if (e.target.files.length > 0) {
                fileNameDisplay.textContent = "ไฟล์ที่เลือก: " + e.target.files[0].name;
                fileNameDisplay.classList.remove('hidden');
                dropzone.classList.add('border-blue-500', 'bg-blue-50');
            } else {
                fileNameDisplay.classList.add('hidden');
                dropzone.classList.remove('border-blue-500', 'bg-blue-50');
            }
        });

        // Form Submission Logic
        const form = document.getElementById('riskForm');
        const toast = document.getElementById('toast');
        const submitBtn = document.getElementById('submitBtn');

        form.addEventListener('submit', (e) => {
            e.preventDefault();
            
            // Validate all fields (extra safety)
            const riskLevel = document.querySelector('input[name="riskLevel"]:checked');
            if (!riskLevel) {
                alert("กรุณาเลือกคะแนนความเสี่ยง");
                return;
            }

            // Visual State: Submitting
            submitBtn.disabled = true;
            submitBtn.textContent = "กำลังบันทึกข้อมูล...";
            submitBtn.classList.add('opacity-50');

            // Simulate Data Sending (e.g., to Google Script)
            setTimeout(() => {
                // Show Success Message
                toast.classList.remove('translate-y-24', 'opacity-0');
                
                // Reset Form
                form.reset();
                fileNameDisplay.classList.add('hidden');
                dropzone.classList.remove('border-blue-500', 'bg-blue-50');
                
                // Restore Button
                submitBtn.disabled = false;
                submitBtn.textContent = "บันทึกรายงานความเสี่ยง";
                submitBtn.classList.remove('opacity-50');

                // Auto-hide Toast
                setTimeout(() => {
                    toast.classList.add('translate-y-24', 'opacity-0');
                }, 4000);

                // Scroll to top
                window.scrollTo({ top: 0, behavior: 'smooth' });
            }, 1500);
        });
    </script>
</body>
</html>
