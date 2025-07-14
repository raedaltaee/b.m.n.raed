<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام إدارة الكيانات الدينية والإدارية</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f3f4f6;
            color: #374151;
            padding: 20px;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background-color: #ffffff;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
        }
        .card {
            background-color: #f9fafb;
            border-radius: 10px;
            padding: 24px;
            margin-bottom: 24px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
            border: 1px solid #e5e7eb;
        }
        .form-input, .form-textarea {
            width: 100%;
            padding: 10px 14px;
            border: 1px solid #d1d5db;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
            background-color: #ffffff;
        }
        .form-input:focus, .form-textarea:focus {
            outline: none;
            border-color: #3b82f6;
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.25);
        }
        .btn {
            padding: 10px 20px;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.2s ease-in-out, transform 0.1s ease-in-out;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        .btn-primary {
            background-color: #3b82f6;
            color: white;
        }
        .btn-primary:hover {
            background-color: #2563eb;
            transform: translateY(-1px);
        }
        .btn-secondary {
            background-color: #6b7280;
            color: white;
        }
        .btn-secondary:hover {
            background-color: #4b5563;
            transform: translateY(-1px);
        }
        .btn-danger {
            background-color: #ef4444;
            color: white;
        }
        .btn-danger:hover {
            background-color: #dc2626;
            transform: translateY(-1px);
        }
        .table-auto {
            width: 100%;
            border-collapse: collapse;
        }
        .table-auto th, .table-auto td {
            padding: 12px 16px;
            border-bottom: 1px solid #e5e7eb;
            text-align: right;
        }
        .table-auto th {
            background-color: #eef2ff;
            font-weight: 600;
            color: #4f46e5;
            text-transform: uppercase;
            font-size: 0.875rem;
        }
        .table-auto tbody tr:hover {
            background-color: #f3f4f6;
        }
        .message-box {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            background-color: #4CAF50;
            color: white;
            padding: 15px 25px;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
            z-index: 1000;
            display: none; /* Hidden by default */
            opacity: 0;
            transition: opacity 0.3s ease-in-out;
            text-align: center;
        }
        .message-box.show {
            display: block;
            opacity: 1;
        }
        .message-box.error {
            background-color: #ef4444;
        }
        .message-box.info {
            background-color: #3b82f6;
        }
    </style>
</head>
<body class="bg-gray-100 p-6">
    <div class="container">
        <!-- قسم المصادقة -->
        <div id="auth-section" class="card text-sm text-gray-600 mb-6 flex justify-between items-center">
            <div>
                <p>مرحباً بك في النظام!</p>
                <p>معرف المستخدم الحالي: <span id="user-id" class="font-mono text-blue-600">جاري التحميل...</span></p>
                <p>حالة المصادقة: <span id="auth-status" class="font-semibold text-gray-700">جاري التحقق...</span></p>
            </div>
            <div>
                <button id="auth-button" class="btn btn-primary">تسجيل الدخول / البدء</button>
            </div>
        </div>

        <!-- صندوق الرسائل المخصص -->
        <div id="messageBox" class="message-box"></div>

        <!-- المحتوى الرئيسي - مخفي حتى يتم المصادقة -->
        <div id="main-content" class="hidden">
            <!-- الجزء الأول: إدارة الكيانات الدينية والتعليمية -->
            <div class="mb-8">
                <h2 class="text-3xl font-bold text-gray-700 mb-6 text-center border-b-2 border-blue-500 pb-2">إدارة الكيانات الدينية والتعليمية</h2>

                <!-- قسم المؤسسات الدينية والخيرية -->
                <div class="card">
                    <h3 class="text-2xl font-semibold text-gray-700 mb-4">المؤسسات الدينية والخيرية</h3>

                    <form id="addInstitutionForm" class="mb-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label for="institutionName" class="block text-gray-700 text-sm font-bold mb-2">اسم المؤسسة:</label>
                                <input type="text" id="institutionName" class="form-input" placeholder="اسم المؤسسة" required>
                            </div>
                            <div>
                                <label for="institutionType" class="block text-gray-700 text-sm font-bold mb-2">النوع:</label>
                                <select id="institutionType" class="form-input" required>
                                    <option value="">اختر النوع</option>
                                    <option value="جامع">جامع</option>
                                    <option value="حسينية">حسينية</option>
                                    <option value="مؤسسة خيرية">مؤسسة خيرية</option>
                                </select>
                            </div>
                            <div>
                                <label for="institutionGov" class="block text-gray-700 text-sm font-bold mb-2">المحافظة:</label>
                                <select id="institutionGov" class="form-input" required>
                                    <option value="">اختر المحافظة</option>
                                    <option value="البصرة">البصرة</option>
                                    <option value="ميسان">ميسان</option>
                                    <option value="ذي قار">ذي قار</option>
                                </select>
                            </div>
                            <div>
                                <label for="institutionLocation" class="block text-gray-700 text-sm font-bold mb-2">الموقع:</label>
                                <input type="text" id="institutionLocation" class="form-input" placeholder="الموقع" required>
                            </div>
                            <div class="md:col-span-2">
                                <label for="institutionCapacity" class="block text-gray-700 text-sm font-bold mb-2">القدرة الاستيعابية (تقريبًا):</label>
                                <input type="number" id="institutionCapacity" class="form-input" placeholder="القدرة الاستيعابية" min="0">
                            </div>

                            <!-- حقول جديدة للمؤسسات -->
                            <div>
                                <label for="institutionEndowmentType" class="block text-gray-700 text-sm font-bold mb-2">نوع الوقف:</label>
                                <input type="text" id="institutionEndowmentType" class="form-input" placeholder="نوع الوقف">
                            </div>
                            <div class="md:col-span-2">
                                <label for="institutionArchitecturalStatus" class="block text-gray-700 text-sm font-bold mb-2">حالته العمرانية:</label>
                                <textarea id="institutionArchitecturalStatus" class="form-textarea" placeholder="وصف الحالة العمرانية"></textarea>
                            </div>
                            <div class="md:col-span-2">
                                <label for="institutionObstacles" class="block text-gray-700 text-sm font-bold mb-2">العقبات:</label>
                                <textarea id="institutionObstacles" class="form-textarea" placeholder="العقبات التي تواجه المؤسسة"></textarea>
                            </div>
                            <div class="md:col-span-2">
                                <label for="institutionNeeds" class="block text-gray-700 text-sm font-bold mb-2">الاحتياجات:</label>
                                <textarea id="institutionNeeds" class="form-textarea" placeholder="احتياجات المؤسسة"></textarea>
                            </div>
                            <div class="md:col-span-2">
                                <label for="institutionSolutions" class="block text-gray-700 text-sm font-bold mb-2">الحلول المقترحة:</label>
                                <textarea id="institutionSolutions" class="form-textarea" placeholder="الحلول المقترحة للعقبات والاحتياجات"></textarea>
                            </div>
                        </div>
                        <button type="submit" class="btn btn-primary mt-4">إضافة مؤسسة</button>
                    </form>

                    <h4 class="text-xl font-semibold text-gray-700 mb-3">المؤسسات الحالية:</h4>
                    <div class="overflow-x-auto rounded-lg shadow">
                        <table class="table-auto">
                            <thead>
                                <tr>
                                    <th>الاسم</th>
                                    <th>النوع</th>
                                    <th>المحافظة</th>
                                    <th>الموقع</th>
                                    <th>القدرة</th>
                                    <th>نوع الوقف</th>
                                    <th>الحالة العمرانية</th>
                                    <th>العقبات</th>
                                    <th>الاحتياجات</th>
                                    <th>الحلول</th>
                                    <th>الإجراءات</th>
                                </tr>
                            </thead>
                            <tbody id="institutionsTableBody">
                                <!-- سيتم تحميل البيانات هنا -->
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- قسم التعليم الديني (المدارس) -->
                <div class="card mt-6">
                    <h3 class="text-2xl font-semibold text-gray-700 mb-4">التعليم الديني (المدارس)</h3>

                    <form id="addSchoolForm" class="mb-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label for="schoolName" class="block text-gray-700 text-sm font-bold mb-2">اسم المدرسة:</label>
                                <input type="text" id="schoolName" class="form-input" placeholder="اسم المدرسة" required>
                            </div>
                            <div>
                                <label for="schoolType" class="block text-gray-700 text-sm font-bold mb-2">النوع:</label>
                                <select id="schoolType" class="form-input" required>
                                    <option value="">اختر النوع</option>
                                    <option value="دينية">دينية</option>
                                    <option value="عامة">عامة</option>
                                </select>
                            </div>
                            <div>
                                <label for="schoolGov" class="block text-gray-700 text-sm font-bold mb-2">المحافظة:</label>
                                <select id="schoolGov" class="form-input" required>
                                    <option value="">اختر المحافظة</option>
                                    <option value="البصرة">البصرة</option>
                                    <option value="ميسان">ميسان</option>
                                    <option value="ذي قار">ذي قار</option>
                                </select>
                            </div>
                            <div>
                                <label for="schoolLocation" class="block text-gray-700 text-sm font-bold mb-2">الموقع:</label>
                                <input type="text" id="schoolLocation" class="form-input" placeholder="الموقع" required>
                            </div>
                            <div>
                                <label for="studentPrimaryMale" class="block text-gray-700 text-sm font-bold mb-2">ذكور ابتدائي:</label>
                                <input type="number" id="studentPrimaryMale" class="form-input" min="0" value="0">
                            </div>
                            <div>
                                <label for="studentPrimaryFemale" class="block text-gray-700 text-sm font-bold mb-2">إناث ابتدائي:</label>
                                <input type="number" id="studentPrimaryFemale" class="form-input" min="0" value="0">
                            </div>
                            <div>
                                <label for="studentIntermediateMale" class="block text-gray-700 text-sm font-bold mb-2">ذكور متوسط:</label>
                                <input type="number" id="studentIntermediateMale" class="form-input" min="0" value="0">
                            </div>
                            <div>
                                <label for="studentIntermediateFemale" class="block text-gray-700 text-sm font-bold mb-2">إناث متوسط:</label>
                                <input type="number" id="studentIntermediateFemale" class="form-input" min="0" value="0">
                            </div>
                            <div>
                                <label for="studentSecondaryMale" class="block text-gray-700 text-sm font-bold mb-2">ذكور ثانوي:</label>
                                <input type="number" id="studentSecondaryMale" class="form-input" min="0" value="0">
                            </div>
                            <div>
                                <label for="studentSecondaryFemale" class="block text-gray-700 text-sm font-bold mb-2">إناث ثانوي:</label>
                                <input type="number" id="studentSecondaryFemale" class="form-input" min="0" value="0">
                            </div>
                            <div class="md:col-span-2">
                                <label for="schoolClassCount" class="block text-gray-700 text-sm font-bold mb-2">عدد الفصول:</label>
                                <input type="number" id="schoolClassCount" class="form-input" min="0" value="0">
                            </div>

                            <!-- حقول جديدة للمدارس -->
                            <div>
                                <label for="schoolAffiliation" class="block text-gray-700 text-sm font-bold mb-2">عائدية المدرسة:</label>
                                <input type="text" id="schoolAffiliation" class="form-input" placeholder="جهة عائدية المدرسة">
                            </div>
                            <div class="md:col-span-2">
                                <label for="schoolArchitecturalStatus" class="block text-gray-700 text-sm font-bold mb-2">حالتها العمرانية:</label>
                                <textarea id="schoolArchitecturalStatus" class="form-textarea" placeholder="وصف الحالة العمرانية للمدرسة"></textarea>
                            </div>
                            <div class="md:col-span-2">
                                <label for="schoolObstacles" class="block text-gray-700 text-sm font-bold mb-2">العقبات:</label>
                                <textarea id="schoolObstacles" class="form-textarea" placeholder="العقبات التي تواجه المدرسة"></textarea>
                            </div>
                            <div class="md:col-span-2">
                                <label for="schoolNeeds" class="block text-gray-700 text-sm font-bold mb-2">الاحتياجات:</label>
                                <textarea id="schoolNeeds" class="form-textarea" placeholder="احتياجات المدرسة"></textarea>
                            </div>
                            <div class="md:col-span-2">
                                <label for="schoolProposedSolutions" class="block text-gray-700 text-sm font-bold mb-2">الحلول المقترحة:</label>
                                <textarea id="schoolProposedSolutions" class="form-textarea" placeholder="الحلول المقترحة للعقبات والاحتياجات"></textarea>
                            </div>
                        </div>
                        <button type="submit" class="btn btn-primary mt-4">إضافة مدرسة</button>
                    </form>

                    <h4 class="text-xl font-semibold text-gray-700 mb-3">المدارس الحالية:</h4>
                    <div class="overflow-x-auto rounded-lg shadow">
                        <table class="table-auto">
                            <thead>
                                <tr>
                                    <th>الاسم</th>
                                    <th>النوع</th>
                                    <th>المحافظة</th>
                                    <th>الموقع</th>
                                    <th>الطلاب (ذ)</th>
                                    <th>الطلاب (إ)</th>
                                    <th>الفصول</th>
                                    <th>العائدية</th>
                                    <th>الحالة العمرانية</th>
                                    <th>العقبات</th>
                                    <th>الاحتياجات</th>
                                    <th>الحلول المقترحة</th>
                                    <th>الإجراءات</th>
                                </tr>
                            </thead>
                            <tbody id="schoolsTableBody">
                                <!-- سيتم تحميل البيانات هنا -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- الجزء الثاني: الشعبة الإدارية -->
            <div class="mb-8">
                <h2 class="text-3xl font-bold text-gray-700 mb-6 text-center border-b-2 border-blue-500 pb-2">الشعبة الإدارية</h2>

                <!-- قسم الموارد الإدارية -->
                <div class="card">
                    <h3 class="text-2xl font-semibold text-gray-700 mb-4">الموارد الإدارية</h3>
                    <form id="addAdministrativeResourceForm" class="mb-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label for="adminEmployeeName" class="block text-gray-700 text-sm font-bold mb-2">اسم الموظف:</label>
                                <input type="text" id="adminEmployeeName" class="form-input" placeholder="اسم الموظف" required>
                            </div>
                            <div>
                                <label for="adminPosition" class="block text-gray-700 text-sm font-bold mb-2">المنصب:</label>
                                <input type="text" id="adminPosition" class="form-input" placeholder="المنصب" required>
                            </div>
                            <div>
                                <label for="adminGov" class="block text-gray-700 text-sm font-bold mb-2">المحافظة:</label>
                                <select id="adminGov" class="form-input" required>
                                    <option value="">اختر المحافظة</option>
                                    <option value="البصرة">البصرة</option>
                                    <option value="ميسان">ميسان</option>
                                    <option value="ذي قار">ذي قار</option>
                                </select>
                            </div>
                            <div>
                                <label for="adminAppointmentDate" class="block text-gray-700 text-sm font-bold mb-2">تاريخ التعيين:</label>
                                <input type="date" id="adminAppointmentDate" class="form-input">
                            </div>
                            <div>
                                <label for="adminLeaveStatus" class="block text-gray-700 text-sm font-bold mb-2">حالة الإجازة:</label>
                                <select id="adminLeaveStatus" class="form-input">
                                    <option value="غير مجاز">غير مجاز</option>
                                    <option value="مجاز">مجاز</option>
                                </select>
                            </div>
                            <div>
                                <label for="adminLeaveType" class="block text-gray-700 text-sm font-bold mb-2">نوع الإجازة (إن وجدت):</label>
                                <input type="text" id="adminLeaveType" class="form-input" placeholder="مثال: إجازة طويلة، إجازة معين">
                            </div>
                            <!-- حقول جديدة للموارد الإدارية -->
                            <div>
                                <label for="adminJobGrade" class="block text-gray-700 text-sm font-bold mb-2">الدرجة الوظيفية:</label>
                                <input type="text" id="adminJobGrade" class="form-input" placeholder="الدرجة الوظيفية">
                            </div>
                            <div>
                                <label for="adminJobCategory" class="block text-gray-700 text-sm font-bold mb-2">الفئة الوظيفية:</label>
                                <input type="text" id="adminJobCategory" class="form-input" placeholder="الفئة الوظيفية">
                            </div>
                            <div class="md:col-span-2">
                                <label for="adminDocumentsUpload" class="block text-gray-700 text-sm font-bold mb-2">المستمسكات (اسم الملف):</label>
                                <input type="text" id="adminDocumentsUpload" class="form-input" placeholder="اسم ملف المستمسك (مثال: هوية_أحمد.pdf)">
                            </div>
                            <div class="md:col-span-2">
                                <label for="adminNotes" class="block text-gray-700 text-sm font-bold mb-2">ملاحظات:</label>
                                <textarea id="adminNotes" class="form-textarea" placeholder="ملاحظات حول الموظف أو حالته"></textarea>
                            </div>
                        </div>
                        <button type="submit" class="btn btn-primary mt-4">إضافة موظف إداري</button>
                    </form>
                    <h4 class="text-xl font-semibold text-gray-700 mb-3">الموظفون الإداريون الحاليون:</h4>
                    <div class="overflow-x-auto rounded-lg shadow">
                        <table class="table-auto">
                            <thead>
                                <tr>
                                    <th>الاسم</th>
                                    <th>المنصب</th>
                                    <th>المحافظة</th>
                                    <th>تاريخ التعيين</th>
                                    <th>حالة الإجازة</th>
                                    <th>نوع الإجازة</th>
                                    <th>الدرجة</th>
                                    <th>الفئة</th>
                                    <th>المستمسكات</th>
                                    <th>ملاحظات</th>
                                    <th>الإجراءات</th>
                                </tr>
                            </thead>
                            <tbody id="administrativeResourcesTableBody">
                                <!-- سيتم تحميل البيانات هنا -->
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- قسم شؤون المواطنين والشكاوى -->
                <div class="card mt-6">
                    <h3 class="text-2xl font-semibold text-gray-700 mb-4">شؤون المواطنين والشكاوى</h3>
                    <form id="addCitizenComplaintForm" class="mb-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label for="complaintNumber" class="block text-gray-700 text-sm font-bold mb-2">رقم الشكوى:</label>
                                <input type="text" id="complaintNumber" class="form-input" placeholder="رقم الشكوى" required>
                            </div>
                            <div>
                                <label for="complaintDate" class="block text-gray-700 text-sm font-bold mb-2">تاريخ الشكوى:</label>
                                <input type="date" id="complaintDate" class="form-input" required>
                            </div>
                            <div>
                                <label for="complainantName" class="block text-gray-700 text-sm font-bold mb-2">اسم المشتكي:</label>
                                <input type="text" id="complainantName" class="form-input" placeholder="اسم المشتكي" required>
                            </div>
                            <div>
                                <label for="complaintGov" class="block text-gray-700 text-sm font-bold mb-2">المحافظة:</label>
                                <select id="complaintGov" class="form-input" required>
                                    <option value="">اختر المحافظة</option>
                                    <option value="البصرة">البصرة</option>
                                    <option value="ميسان">ميسان</option>
                                    <option value="ذي قار">ذي قار</option>
                                </select>
                            </div>
                            <div class="md:col-span-2">
                                <label for="complaintSubject" class="block text-gray-700 text-sm font-bold mb-2">موضوع الشكوى:</label>
                                <textarea id="complaintSubject" class="form-textarea" placeholder="موضوع الشكوى" required></textarea>
                            </div>
                            <div>
                                <label for="complaintStatus" class="block text-gray-700 text-sm font-bold mb-2">حالة الشكوى:</label>
                                <select id="complaintStatus" class="form-input">
                                    <option value="قيد المراجعة">قيد المراجعة</option>
                                    <option value="تم الحل">تم الحل</option>
                                    <option value="معلقة">معلقة</option>
                                    <option value="تم الرفض">تم الرفض</option>
                                </select>
                            </div>
                            <div class="md:col-span-2">
                                <label for="complaintNotes" class="block text-gray-700 text-sm font-bold mb-2">ملاحظات:</label>
                                <textarea id="complaintNotes" class="form-textarea" placeholder="ملاحظات إضافية حول الشكوى"></textarea>
                            </div>
                        </div>
                        <button type="submit" class="btn btn-primary mt-4">إضافة شكوى</button>
                    </form>

                    <h4 class="text-xl font-semibold text-gray-700 mb-3">الشكاوى الحالية:</h4>
                    <div class="overflow-x-auto rounded-lg shadow">
                        <table class="table-auto">
                            <thead>
                                <tr>
                                    <th>رقم الشكوى</th>
                                    <th>التاريخ</th>
                                    <th>اسم المشتكي</th>
                                    <th>المحافظة</th>
                                    <th>الموضوع</th>
                                    <th>الحالة</th>
                                    <th>ملاحظات</th>
                                    <th>الإجراءات</th>
                                </tr>
                            </thead>
                            <tbody id="citizenComplaintsTableBody">
                                <!-- سيتم تحميل البيانات هنا -->
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- قسم البريد الوارد -->
                <div class="card mt-6">
                    <h3 class="text-2xl font-semibold text-gray-700 mb-4">البريد الوارد</h3>
                    <form id="addIncomingMailForm" class="mb-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label for="incomingMailLetterNumber" class="block text-gray-700 text-sm font-bold mb-2">رقم الكتاب:</label>
                                <input type="text" id="incomingMailLetterNumber" class="form-input" placeholder="رقم الكتاب الوارد" required>
                            </div>
                            <div>
                                <label for="incomingMailLetterDate" class="block text-gray-700 text-sm font-bold mb-2">تاريخ الكتاب:</label>
                                <input type="date" id="incomingMailLetterDate" class="form-input" required>
                            </div>
                            <div>
                                <label for="incomingMailSender" class="block text-gray-700 text-sm font-bold mb-2">الجهة المرسلة:</label>
                                <input type="text" id="incomingMailSender" class="form-input" placeholder="اسم الجهة المرسلة" required>
                            </div>
                            <div>
                                <label for="incomingMailGov" class="block text-gray-700 text-sm font-bold mb-2">المحافظة:</label>
                                <select id="incomingMailGov" class="form-input" required>
                                    <option value="">اختر المحافظة</option>
                                    <option value="البصرة">البصرة</option>
                                    <option value="ميسان">ميسان</option>
                                    <option value="ذي قار">ذي قار</option>
                                </select>
                            </div>
                            <div class="md:col-span-2">
                                <label for="incomingMailSubject" class="block text-gray-700 text-sm font-bold mb-2">الموضوع:</label>
                                <textarea id="incomingMailSubject" class="form-textarea" placeholder="موضوع الكتاب الوارد" required></textarea>
                            </div>
                            <div>
                                <label for="incomingMailFollowupStatus" class="block text-gray-700 text-sm font-bold mb-2">حالة المتابعة:</label>
                                <input type="text" id="incomingMailFollowupStatus" class="form-input" placeholder="حالة المتابعة">
                            </div>
                            <div class="md:col-span-2">
                                <label for="incomingMailNotes" class="block text-gray-700 text-sm font-bold mb-2">ملاحظات:</label>
                                <textarea id="incomingMailNotes" class="form-textarea" placeholder="ملاحظات إضافية"></textarea>
                            </div>
                        </div>
                        <button type="submit" class="btn btn-primary mt-4">إضافة كتاب وارد</button>
                    </form>
                    
                    <div class="flex flex-col md:flex-row gap-4 mb-4">
                        <input type="text" id="incomingMailSearchQuery" class="form-input flex-grow md:w-auto" placeholder="بحث بالرقم، التاريخ، الموضوع، الجهة المرسلة...">
                        <button id="searchIncomingMailBtn" class="btn btn-secondary flex-shrink-0">بحث</button>
                    </div>

                    <h4 class="text-xl font-semibold text-gray-700 mb-3">الكتب الواردة الحالية:</h4>
                    <div class="overflow-x-auto rounded-lg shadow">
                        <table class="table-auto">
                            <thead>
                                <tr>
                                    <th>رقم الكتاب</th>
                                    <th>تاريخه</th>
                                    <th>المرسل</th>
                                    <th>المحافظة</th>
                                    <th>الموضوع</th>
                                    <th>حالة المتابعة</th>
                                    <th>ملاحظات</th>
                                    <th>الإجراءات</th>
                                </tr>
                            </thead>
                            <tbody id="incomingMailTableBody">
                                <!-- سيتم تحميل البيانات هنا -->
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- قسم البريد الصادر -->
                <div class="card mt-6">
                    <h3 class="text-2xl font-semibold text-gray-700 mb-4">البريد الصادر</h3>
                    <form id="addOutgoingMailForm" class="mb-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label for="outgoingMailLetterNumber" class="block text-gray-700 text-sm font-bold mb-2">رقم الكتاب:</label>
                                <input type="text" id="outgoingMailLetterNumber" class="form-input" placeholder="رقم الكتاب الصادر" required>
                            </div>
                            <div>
                                <label for="outgoingMailLetterDate" class="block text-gray-700 text-sm font-bold mb-2">تاريخ الكتاب:</label>
                                <input type="date" id="outgoingMailLetterDate" class="form-input" required>
                            </div>
                            <div>
                                <label for="outgoingMailRecipient" class="block text-gray-700 text-sm font-bold mb-2">الجهة الصادر إليها:</label>
                                <input type="text" id="outgoingMailRecipient" class="form-input" placeholder="اسم الجهة الصادر إليها" required>
                            </div>
                            <div>
                                <label for="outgoingMailGov" class="block text-gray-700 text-sm font-bold mb-2">المحافظة:</label>
                                <select id="outgoingMailGov" class="form-input" required>
                                    <option value="">اختر المحافظة</option>
                                    <option value="البصرة">البصرة</option>
                                    <option value="ميسان">ميسان</option>
                                    <option value="ذي قار">ذي قار</option>
                                </select>
                            </div>
                            <div class="md:col-span-2">
                                <label for="outgoingMailSubject" class="block text-gray-700 text-sm font-bold mb-2">الموضوع:</label>
                                <textarea id="outgoingMailSubject" class="form-textarea" placeholder="موضوع الكتاب الصادر" required></textarea>
                            </div>
                            <div>
                                <label for="outgoingMailFollowupStatus" class="block text-gray-700 text-sm font-bold mb-2">حالة المتابعة:</label>
                                <input type="text" id="outgoingMailFollowupStatus" class="form-input" placeholder="حالة المتابعة">
                            </div>
                            <div class="md:col-span-2">
                                <label for="outgoingMailNotes" class="block text-gray-700 text-sm font-bold mb-2">ملاحظات:</label>
                                <textarea id="outgoingMailNotes" class="form-textarea" placeholder="ملاحظات إضافية"></textarea>
                            </div>
                        </div>
                        <button type="submit" class="btn btn-primary mt-4">إضافة كتاب صادر</button>
                    </form>

                    <div class="flex flex-col md:flex-row gap-4 mb-4">
                        <input type="text" id="outgoingMailSearchQuery" class="form-input flex-grow md:w-auto" placeholder="بحث بالرقم، التاريخ، الموضوع، الجهة الصادر إليها...">
                        <button id="searchOutgoingMailBtn" class="btn btn-secondary flex-shrink-0">بحث</button>
                    </div>

                    <h4 class="text-xl font-semibold text-gray-700 mb-3">الكتب الصادرة الحالية:</h4>
                    <div class="overflow-x-auto rounded-lg shadow">
                        <table class="table-auto">
                            <thead>
                                <tr>
                                    <th>رقم الكتاب</th>
                                    <th>تاريخه</th>
                                    <th>الجهة الصادرة إليها</th>
                                    <th>المحافظة</th>
                                    <th>الموضوع</th>
                                    <th>حالة المتابعة</th>
                                    <th>ملاحظات</th>
                                    <th>الإجراءات</th>
                                </tr>
                            </thead>
                            <tbody id="outgoingMailTableBody">
                                <!-- سيتم تحميل البيانات هنا -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script type="module">
        // استيراد وحدات Firebase الضرورية
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, getDoc, addDoc, setDoc, updateDoc, deleteDoc, onSnapshot, collection, query, where, getDocs } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // تهيئة Firebase
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');
        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);
        const auth = getAuth(app);

        let userId = null; // متغير لتخزين معرف المستخدم الحالي
        let isAuthReady = false; // لتتبع ما إذا كانت المصادقة جاهزة

        // عناصر واجهة المستخدم
        const userIdSpan = document.getElementById('user-id');
        const authStatusSpan = document.getElementById('auth-status');
        const authButton = document.getElementById('auth-button');
        const mainContent = document.getElementById('main-content');
        const messageBox = document.getElementById('messageBox');

        // جداول البيانات
        const institutionsTableBody = document.getElementById('institutionsTableBody');
        const schoolsTableBody = document.getElementById('schoolsTableBody');
        const administrativeResourcesTableBody = document.getElementById('administrativeResourcesTableBody');
        const citizenComplaintsTableBody = document.getElementById('citizenComplaintsTableBody');
        const incomingMailTableBody = document.getElementById('incomingMailTableBody');
        const outgoingMailTableBody = document.getElementById('outgoingMailTableBody');

        /**
         * يعرض رسالة في صندوق الرسائل المخصص.
         * @param {string} message - الرسالة المراد عرضها.
         * @param {string} type - نوع الرسالة ('success', 'error', 'info').
         */
        function showMessage(message, type = 'success') {
            messageBox.textContent = message;
            messageBox.className = `message-box show ${type}`;
            setTimeout(() => {
                messageBox.classList.remove('show');
            }, 3000);
        }

        /**
         * يتعامل مع تغيير حالة المصادقة.
         * @param {object} user - كائن المستخدم الحالي من Firebase Auth.
         */
        onAuthStateChanged(auth, async (user) => {
            if (user) {
                userId = user.uid;
                userIdSpan.textContent = userId;
                authStatusSpan.textContent = 'مصادق عليه';
                mainContent.classList.remove('hidden');
                authButton.textContent = 'تسجيل الخروج';
                showMessage('تم تسجيل الدخول بنجاح!', 'success');

                // تحميل البيانات بعد المصادقة
                loadInstitutions();
                loadSchools();
                loadAdministrativeResources();
                loadCitizenComplaints();
                loadIncomingMail();
                loadOutgoingMail();
            } else {
                userId = null;
                userIdSpan.textContent = 'غير متوفر';
                authStatusSpan.textContent = 'غير مصادق عليه';
                mainContent.classList.add('hidden');
                authButton.textContent = 'تسجيل الدخول / البدء';
                showMessage('يرجى تسجيل الدخول للوصول إلى التطبيق.', 'info');
            }
            isAuthReady = true; // تعيين المصادقة كجاهزة
        });

        /**
         * يتعامل مع زر المصادقة (تسجيل الدخول/الخروج).
         */
        authButton.addEventListener('click', async () => {
            if (userId) {
                // إذا كان المستخدم مسجلاً للدخول، قم بتسجيل الخروج
                try {
                    await signOut(auth);
                    showMessage('تم تسجيل الخروج بنجاح.', 'success');
                } catch (error) {
                    console.error("خطأ في تسجيل الخروج:", error);
                    showMessage('خطأ في تسجيل الخروج: ' + error.message, 'error');
                }
            } else {
                // إذا لم يكن المستخدم مسجلاً للدخول، قم بتسجيل الدخول
                try {
                    if (typeof __initial_auth_token !== 'undefined') {
                        await signInWithCustomToken(auth, __initial_auth_token);
                    } else {
                        await signInAnonymously(auth);
                    }
                    // لا حاجة لرسالة هنا، onAuthStateChanged سيتولى الأمر
                } catch (error) {
                    console.error("خطأ في المصادقة:", error);
                    showMessage('خطأ في المصادقة: ' + error.message, 'error');
                }
            }
        });

        /**
         * يحصل على مسار مجموعة البيانات (خاص بالمستخدم).
         * @param {string} collectionName - اسم المجموعة.
         * @returns {string} - المسار الكامل للمجموعة.
         */
        function getUserCollectionPath(collectionName) {
            return `artifacts/${appId}/users/${userId}/${collectionName}`;
        }

        /**
         * يحصل على مسار وثيقة معينة (خاص بالمستخدم).
         * @param {string} collectionName - اسم المجموعة.
         * @param {string} docId - معرف الوثيقة.
         * @returns {object} - مرجع الوثيقة.
         */
        function getUserDocRef(collectionName, docId) {
            return doc(db, getUserCollectionPath(collectionName), docId);
        }

        // --- وظائف إدارة المؤسسات الدينية والخيرية ---

        /**
         * يحمل ويعرض المؤسسات الدينية والخيرية.
         */
        function loadInstitutions() {
            if (!isAuthReady || !userId) return; // تأكد من أن المصادقة جاهزة وأن هناك معرف مستخدم

            const q = query(collection(db, getUserCollectionPath('institutions')));
            onSnapshot(q, (snapshot) => {
                institutionsTableBody.innerHTML = ''; // مسح الجدول الحالي
                snapshot.forEach((doc) => {
                    const data = doc.data();
                    const row = institutionsTableBody.insertRow();
                    row.insertCell().textContent = data.name;
                    row.insertCell().textContent = data.type;
                    row.insertCell().textContent = data.gov;
                    row.insertCell().textContent = data.location;
                    row.insertCell().textContent = data.capacity || '';
                    row.insertCell().textContent = data.endowmentType || '';
                    row.insertCell().textContent = data.architecturalStatus || '';
                    row.insertCell().textContent = data.obstacles || '';
                    row.insertCell().textContent = data.needs || '';
                    row.insertCell().textContent = data.solutions || '';

                    const actionsCell = row.insertCell();
                    const editButton = document.createElement('button');
                    editButton.textContent = 'تعديل';
                    editButton.className = 'btn btn-secondary text-xs ml-2';
                    editButton.onclick = () => editInstitution(doc.id, data);
                    actionsCell.appendChild(editButton);

                    const deleteButton = document.createElement('button');
                    deleteButton.textContent = 'حذف';
                    deleteButton.className = 'btn btn-danger text-xs';
                    deleteButton.onclick = () => deleteDocument('institutions', doc.id);
                    actionsCell.appendChild(deleteButton);
                });
            }, (error) => {
                console.error("خطأ في تحميل المؤسسات:", error);
                showMessage('خطأ في تحميل المؤسسات: ' + error.message, 'error');
            });
        }

        /**
         * يضيف مؤسسة دينية أو خيرية جديدة.
         */
        document.getElementById('addInstitutionForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            if (!userId) {
                showMessage('يرجى تسجيل الدخول لإضافة مؤسسة.', 'info');
                return;
            }
            const name = document.getElementById('institutionName').value;
            const type = document.getElementById('institutionType').value;
            const gov = document.getElementById('institutionGov').value;
            const location = document.getElementById('institutionLocation').value;
            const capacity = document.getElementById('institutionCapacity').value;
            const endowmentType = document.getElementById('institutionEndowmentType').value;
            const architecturalStatus = document.getElementById('institutionArchitecturalStatus').value;
            const obstacles = document.getElementById('institutionObstacles').value;
            const needs = document.getElementById('institutionNeeds').value;
            const solutions = document.getElementById('institutionSolutions').value;

            try {
                await addDoc(collection(db, getUserCollectionPath('institutions')), {
                    name, type, gov, location, capacity: parseInt(capacity) || 0,
                    endowmentType, architecturalStatus, obstacles, needs, solutions,
                    createdAt: new Date()
                });
                showMessage('تمت إضافة المؤسسة بنجاح!', 'success');
                e.target.reset(); // مسح النموذج
            } catch (e) {
                console.error("خطأ في إضافة المؤسسة:", e);
                showMessage('خطأ في إضافة المؤسسة: ' + e.message, 'error');
            }
        });

        /**
         * يفتح نموذج تعديل المؤسسة.
         * @param {string} id - معرف الوثيقة.
         * @param {object} data - بيانات المؤسسة الحالية.
         */
        function editInstitution(id, data) {
            const form = document.getElementById('addInstitutionForm');
            document.getElementById('institutionName').value = data.name;
            document.getElementById('institutionType').value = data.type;
            document.getElementById('institutionGov').value = data.gov;
            document.getElementById('institutionLocation').value = data.location;
            document.getElementById('institutionCapacity').value = data.capacity;
            document.getElementById('institutionEndowmentType').value = data.endowmentType || '';
            document.getElementById('institutionArchitecturalStatus').value = data.architecturalStatus || '';
            document.getElementById('institutionObstacles').value = data.obstacles || '';
            document.getElementById('institutionNeeds').value = data.needs || '';
            document.getElementById('institutionSolutions').value = data.solutions || '';

            const submitButton = form.querySelector('button[type="submit"]');
            submitButton.textContent = 'تحديث المؤسسة';
            submitButton.onclick = async (e) => {
                e.preventDefault();
                try {
                    await updateDoc(getUserDocRef('institutions', id), {
                        name: document.getElementById('institutionName').value,
                        type: document.getElementById('institutionType').value,
                        gov: document.getElementById('institutionGov').value,
                        location: document.getElementById('institutionLocation').value,
                        capacity: parseInt(document.getElementById('institutionCapacity').value) || 0,
                        endowmentType: document.getElementById('institutionEndowmentType').value,
                        architecturalStatus: document.getElementById('institutionArchitecturalStatus').value,
                        obstacles: document.getElementById('institutionObstacles').value,
                        needs: document.getElementById('institutionNeeds').value,
                        solutions: document.getElementById('institutionSolutions').value
                    });
                    showMessage('تم تحديث المؤسسة بنجاح!', 'success');
                    form.reset();
                    submitButton.textContent = 'إضافة مؤسسة';
                    submitButton.onclick = null; // إزالة معالج الأحداث المؤقت
                } catch (e) {
                    console.error("خطأ في تحديث المؤسسة:", e);
                    showMessage('خطأ في تحديث المؤسسة: ' + e.message, 'error');
                }
            };
        }

        // --- وظائف إدارة التعليم الديني (المدارس) ---

        /**
         * يحمل ويعرض المدارس الدينية.
         */
        function loadSchools() {
            if (!isAuthReady || !userId) return;

            const q = query(collection(db, getUserCollectionPath('schools')));
            onSnapshot(q, (snapshot) => {
                schoolsTableBody.innerHTML = '';
                snapshot.forEach((doc) => {
                    const data = doc.data();
                    const row = schoolsTableBody.insertRow();
                    row.insertCell().textContent = data.name;
                    row.insertCell().textContent = data.type;
                    row.insertCell().textContent = data.gov;
                    row.insertCell().textContent = data.location;
                    row.insertCell().textContent = data.studentPrimaryMale || 0;
                    row.insertCell().textContent = data.studentPrimaryFemale || 0;
                    row.insertCell().textContent = data.schoolClassCount || 0;
                    row.insertCell().textContent = data.affiliation || '';
                    row.insertCell().textContent = data.architecturalStatus || '';
                    row.insertCell().textContent = data.obstacles || '';
                    row.insertCell().textContent = data.needs || '';
                    row.insertCell().textContent = data.proposedSolutions || '';

                    const actionsCell = row.insertCell();
                    const editButton = document.createElement('button');
                    editButton.textContent = 'تعديل';
                    editButton.className = 'btn btn-secondary text-xs ml-2';
                    editButton.onclick = () => editSchool(doc.id, data);
                    actionsCell.appendChild(editButton);

                    const deleteButton = document.createElement('button');
                    deleteButton.textContent = 'حذف';
                    deleteButton.className = 'btn btn-danger text-xs';
                    deleteButton.onclick = () => deleteDocument('schools', doc.id);
                    actionsCell.appendChild(deleteButton);
                });
            }, (error) => {
                console.error("خطأ في تحميل المدارس:", error);
                showMessage('خطأ في تحميل المدارس: ' + error.message, 'error');
            });
        }

        /**
         * يضيف مدرسة دينية جديدة.
         */
        document.getElementById('addSchoolForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            if (!userId) {
                showMessage('يرجى تسجيل الدخول لإضافة مدرسة.', 'info');
                return;
            }
            const name = document.getElementById('schoolName').value;
            const type = document.getElementById('schoolType').value;
            const gov = document.getElementById('schoolGov').value;
            const location = document.getElementById('schoolLocation').value;
            const studentPrimaryMale = parseInt(document.getElementById('studentPrimaryMale').value) || 0;
            const studentPrimaryFemale = parseInt(document.getElementById('studentPrimaryFemale').value) || 0;
            const studentIntermediateMale = parseInt(document.getElementById('studentIntermediateMale').value) || 0;
            const studentIntermediateFemale = parseInt(document.getElementById('studentIntermediateFemale').value) || 0;
            const studentSecondaryMale = parseInt(document.getElementById('studentSecondaryMale').value) || 0;
            const studentSecondaryFemale = parseInt(document.getElementById('studentSecondaryFemale').value) || 0;
            const schoolClassCount = parseInt(document.getElementById('schoolClassCount').value) || 0;
            const affiliation = document.getElementById('schoolAffiliation').value;
            const architecturalStatus = document.getElementById('schoolArchitecturalStatus').value;
            const obstacles = document.getElementById('schoolObstacles').value;
            const needs = document.getElementById('schoolNeeds').value;
            const proposedSolutions = document.getElementById('schoolProposedSolutions').value;

            try {
                await addDoc(collection(db, getUserCollectionPath('schools')), {
                    name, type, gov, location, studentPrimaryMale, studentPrimaryFemale,
                    studentIntermediateMale, studentIntermediateFemale, studentSecondaryMale,
                    studentSecondaryFemale, schoolClassCount, affiliation, architecturalStatus,
                    obstacles, needs, proposedSolutions,
                    createdAt: new Date()
                });
                showMessage('تمت إضافة المدرسة بنجاح!', 'success');
                e.target.reset();
            } catch (e) {
                console.error("خطأ في إضافة المدرسة:", e);
                showMessage('خطأ في إضافة المدرسة: ' + e.message, 'error');
            }
        });

        /**
         * يفتح نموذج تعديل المدرسة.
         * @param {string} id - معرف الوثيقة.
         * @param {object} data - بيانات المدرسة الحالية.
         */
        function editSchool(id, data) {
            const form = document.getElementById('addSchoolForm');
            document.getElementById('schoolName').value = data.name;
            document.getElementById('schoolType').value = data.type;
            document.getElementById('schoolGov').value = data.gov;
            document.getElementById('schoolLocation').value = data.location;
            document.getElementById('studentPrimaryMale').value = data.studentPrimaryMale || 0;
            document.getElementById('studentPrimaryFemale').value = data.studentPrimaryFemale || 0;
            document.getElementById('studentIntermediateMale').value = data.studentIntermediateMale || 0;
            document.getElementById('studentIntermediateFemale').value = data.studentIntermediateFemale || 0;
            document.getElementById('studentSecondaryMale').value = data.studentSecondaryMale || 0;
            document.getElementById('studentSecondaryFemale').value = data.studentSecondaryFemale || 0;
            document.getElementById('schoolClassCount').value = data.schoolClassCount || 0;
            document.getElementById('schoolAffiliation').value = data.affiliation || '';
            document.getElementById('schoolArchitecturalStatus').value = data.architecturalStatus || '';
            document.getElementById('schoolObstacles').value = data.obstacles || '';
            document.getElementById('schoolNeeds').value = data.needs || '';
            document.getElementById('schoolProposedSolutions').value = data.proposedSolutions || '';

            const submitButton = form.querySelector('button[type="submit"]');
            submitButton.textContent = 'تحديث المدرسة';
            submitButton.onclick = async (e) => {
                e.preventDefault();
                try {
                    await updateDoc(getUserDocRef('schools', id), {
                        name: document.getElementById('schoolName').value,
                        type: document.getElementById('schoolType').value,
                        gov: document.getElementById('schoolGov').value,
                        location: document.getElementById('schoolLocation').value,
                        studentPrimaryMale: parseInt(document.getElementById('studentPrimaryMale').value) || 0,
                        studentPrimaryFemale: parseInt(document.getElementById('studentPrimaryFemale').value) || 0,
                        studentIntermediateMale: parseInt(document.getElementById('studentIntermediateMale').value) || 0,
                        studentIntermediateFemale: parseInt(document.getElementById('studentIntermediateFemale').value) || 0,
                        studentSecondaryMale: parseInt(document.getElementById('studentSecondaryMale').value) || 0,
                        studentSecondaryFemale: parseInt(document.getElementById('studentSecondaryFemale').value) || 0,
                        schoolClassCount: parseInt(document.getElementById('schoolClassCount').value) || 0,
                        affiliation: document.getElementById('schoolAffiliation').value,
                        architecturalStatus: document.getElementById('schoolArchitecturalStatus').value,
                        obstacles: document.getElementById('schoolObstacles').value,
                        needs: document.getElementById('schoolNeeds').value,
                        proposedSolutions: document.getElementById('schoolProposedSolutions').value
                    });
                    showMessage('تم تحديث المدرسة بنجاح!', 'success');
                    form.reset();
                    submitButton.textContent = 'إضافة مدرسة';
                    submitButton.onclick = null;
                } catch (e) {
                    console.error("خطأ في تحديث المدرسة:", e);
                    showMessage('خطأ في تحديث المدرسة: ' + e.message, 'error');
                }
            };
        }

        // --- وظائف إدارة الموارد الإدارية ---

        /**
         * يحمل ويعرض الموارد الإدارية.
         */
        function loadAdministrativeResources() {
            if (!isAuthReady || !userId) return;

            const q = query(collection(db, getUserCollectionPath('administrativeResources')));
            onSnapshot(q, (snapshot) => {
                administrativeResourcesTableBody.innerHTML = '';
                snapshot.forEach((doc) => {
                    const data = doc.data();
                    const row = administrativeResourcesTableBody.insertRow();
                    row.insertCell().textContent = data.employeeName;
                    row.insertCell().textContent = data.position;
                    row.insertCell().textContent = data.gov;
                    row.insertCell().textContent = data.appointmentDate;
                    row.insertCell().textContent = data.leaveStatus;
                    row.insertCell().textContent = data.leaveType || '';
                    row.insertCell().textContent = data.jobGrade || '';
                    row.insertCell().textContent = data.jobCategory || '';
                    row.insertCell().textContent = data.documentsUpload || '';
                    row.insertCell().textContent = data.notes || '';

                    const actionsCell = row.insertCell();
                    const editButton = document.createElement('button');
                    editButton.textContent = 'تعديل';
                    editButton.className = 'btn btn-secondary text-xs ml-2';
                    editButton.onclick = () => editAdministrativeResource(doc.id, data);
                    actionsCell.appendChild(editButton);

                    const deleteButton = document.createElement('button');
                    deleteButton.textContent = 'حذف';
                    deleteButton.className = 'btn btn-danger text-xs';
                    deleteButton.onclick = () => deleteDocument('administrativeResources', doc.id);
                    actionsCell.appendChild(deleteButton);
                });
            }, (error) => {
                console.error("خطأ في تحميل الموارد الإدارية:", error);
                showMessage('خطأ في تحميل الموارد الإدارية: ' + error.message, 'error');
            });
        }

        /**
         * يضيف موظف إداري جديد.
         */
        document.getElementById('addAdministrativeResourceForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            if (!userId) {
                showMessage('يرجى تسجيل الدخول لإضافة موظف إداري.', 'info');
                return;
            }
            const employeeName = document.getElementById('adminEmployeeName').value;
            const position = document.getElementById('adminPosition').value;
            const gov = document.getElementById('adminGov').value;
            const appointmentDate = document.getElementById('adminAppointmentDate').value;
            const leaveStatus = document.getElementById('adminLeaveStatus').value;
            const leaveType = document.getElementById('adminLeaveType').value;
            const jobGrade = document.getElementById('adminJobGrade').value;
            const jobCategory = document.getElementById('adminJobCategory').value;
            const documentsUpload = document.getElementById('adminDocumentsUpload').value;
            const notes = document.getElementById('adminNotes').value;

            try {
                await addDoc(collection(db, getUserCollectionPath('administrativeResources')), {
                    employeeName, position, gov, appointmentDate, leaveStatus, leaveType,
                    jobGrade, jobCategory, documentsUpload, notes,
                    createdAt: new Date()
                });
                showMessage('تمت إضافة الموظف الإداري بنجاح!', 'success');
                e.target.reset();
            } catch (e) {
                console.error("خطأ في إضافة الموظف الإداري:", e);
                showMessage('خطأ في إضافة الموظف الإداري: ' + e.message, 'error');
            }
        });

        /**
         * يفتح نموذج تعديل المورد الإداري.
         * @param {string} id - معرف الوثيقة.
         * @param {object} data - بيانات المورد الإداري الحالية.
         */
        function editAdministrativeResource(id, data) {
            const form = document.getElementById('addAdministrativeResourceForm');
            document.getElementById('adminEmployeeName').value = data.employeeName;
            document.getElementById('adminPosition').value = data.position;
            document.getElementById('adminGov').value = data.gov;
            document.getElementById('adminAppointmentDate').value = data.appointmentDate;
            document.getElementById('adminLeaveStatus').value = data.leaveStatus;
            document.getElementById('adminLeaveType').value = data.leaveType || '';
            document.getElementById('adminJobGrade').value = data.jobGrade || '';
            document.getElementById('adminJobCategory').value = data.jobCategory || '';
            document.getElementById('adminDocumentsUpload').value = data.documentsUpload || '';
            document.getElementById('adminNotes').value = data.notes || '';

            const submitButton = form.querySelector('button[type="submit"]');
            submitButton.textContent = 'تحديث الموظف الإداري';
            submitButton.onclick = async (e) => {
                e.preventDefault();
                try {
                    await updateDoc(getUserDocRef('administrativeResources', id), {
                        employeeName: document.getElementById('adminEmployeeName').value,
                        position: document.getElementById('adminPosition').value,
                        gov: document.getElementById('adminGov').value,
                        appointmentDate: document.getElementById('adminAppointmentDate').value,
                        leaveStatus: document.getElementById('adminLeaveStatus').value,
                        leaveType: document.getElementById('adminLeaveType').value,
                        jobGrade: document.getElementById('adminJobGrade').value,
                        jobCategory: document.getElementById('adminJobCategory').value,
                        documentsUpload: document.getElementById('adminDocumentsUpload').value,
                        notes: document.getElementById('adminNotes').value
                    });
                    showMessage('تم تحديث الموظف الإداري بنجاح!', 'success');
                    form.reset();
                    submitButton.textContent = 'إضافة موظف إداري';
                    submitButton.onclick = null;
                } catch (e) {
                    console.error("خطأ في تحديث الموظف الإداري:", e);
                    showMessage('خطأ في تحديث الموظف الإداري: ' + e.message, 'error');
                }
            };
        }

        // --- وظائف إدارة شؤون المواطنين والشكاوى ---

        /**
         * يحمل ويعرض شكاوى المواطنين.
         */
        function loadCitizenComplaints() {
            if (!isAuthReady || !userId) return;

            const q = query(collection(db, getUserCollectionPath('citizenComplaints')));
            onSnapshot(q, (snapshot) => {
                citizenComplaintsTableBody.innerHTML = '';
                snapshot.forEach((doc) => {
                    const data = doc.data();
                    const row = citizenComplaintsTableBody.insertRow();
                    row.insertCell().textContent = data.complaintNumber;
                    row.insertCell().textContent = data.complaintDate;
                    row.insertCell().textContent = data.complainantName;
                    row.insertCell().textContent = data.complaintGov;
                    row.insertCell().textContent = data.complaintSubject;
                    row.insertCell().textContent = data.complaintStatus;
                    row.insertCell().textContent = data.complaintNotes || '';

                    const actionsCell = row.insertCell();
                    const editButton = document.createElement('button');
                    editButton.textContent = 'تعديل';
                    editButton.className = 'btn btn-secondary text-xs ml-2';
                    editButton.onclick = () => editCitizenComplaint(doc.id, data);
                    actionsCell.appendChild(editButton);

                    const deleteButton = document.createElement('button');
                    deleteButton.textContent = 'حذف';
                    deleteButton.className = 'btn btn-danger text-xs';
                    deleteButton.onclick = () => deleteDocument('citizenComplaints', doc.id);
                    actionsCell.appendChild(deleteButton);
                });
            }, (error) => {
                console.error("خطأ في تحميل الشكاوى:", error);
                showMessage('خطأ في تحميل الشكاوى: ' + error.message, 'error');
            });
        }

        /**
         * يضيف شكوى مواطن جديدة.
         */
        document.getElementById('addCitizenComplaintForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            if (!userId) {
                showMessage('يرجى تسجيل الدخول لإضافة شكوى.', 'info');
                return;
            }
            const complaintNumber = document.getElementById('complaintNumber').value;
            const complaintDate = document.getElementById('complaintDate').value;
            const complainantName = document.getElementById('complainantName').value;
            const complaintGov = document.getElementById('complaintGov').value;
            const complaintSubject = document.getElementById('complaintSubject').value;
            const complaintStatus = document.getElementById('complaintStatus').value;
            const complaintNotes = document.getElementById('complaintNotes').value;

            try {
                await addDoc(collection(db, getUserCollectionPath('citizenComplaints')), {
                    complaintNumber, complaintDate, complainantName, complaintGov,
                    complaintSubject, complaintStatus, complaintNotes,
                    createdAt: new Date()
                });
                showMessage('تمت إضافة الشكوى بنجاح!', 'success');
                e.target.reset();
            } catch (e) {
                console.error("خطأ في إضافة الشكوى:", e);
                showMessage('خطأ في إضافة الشكوى: ' + e.message, 'error');
            }
        });

        /**
         * يفتح نموذج تعديل شكوى المواطن.
         * @param {string} id - معرف الوثيقة.
         * @param {object} data - بيانات الشكوى الحالية.
         */
        function editCitizenComplaint(id, data) {
            const form = document.getElementById('addCitizenComplaintForm');
            document.getElementById('complaintNumber').value = data.complaintNumber;
            document.getElementById('complaintDate').value = data.complaintDate;
            document.getElementById('complainantName').value = data.complainantName;
            document.getElementById('complaintGov').value = data.complaintGov;
            document.getElementById('complaintSubject').value = data.complaintSubject;
            document.getElementById('complaintStatus').value = data.complaintStatus;
            document.getElementById('complaintNotes').value = data.complaintNotes || '';

            const submitButton = form.querySelector('button[type="submit"]');
            submitButton.textContent = 'تحديث الشكوى';
            submitButton.onclick = async (e) => {
                e.preventDefault();
                try {
                    await updateDoc(getUserDocRef('citizenComplaints', id), {
                        complaintNumber: document.getElementById('complaintNumber').value,
                        complaintDate: document.getElementById('complaintDate').value,
                        complainantName: document.getElementById('complainantName').value,
                        complaintGov: document.getElementById('complaintGov').value,
                        complaintSubject: document.getElementById('complaintSubject').value,
                        complaintStatus: document.getElementById('complaintStatus').value,
                        complaintNotes: document.getElementById('complaintNotes').value
                    });
                    showMessage('تم تحديث الشكوى بنجاح!', 'success');
                    form.reset();
                    submitButton.textContent = 'إضافة شكوى';
                    submitButton.onclick = null;
                } catch (e) {
                    console.error("خطأ في تحديث الشكوى:", e);
                    showMessage('خطأ في تحديث الشكوى: ' + e.message, 'error');
                }
            };
        }

        // --- وظائف إدارة البريد الوارد ---

        /**
         * يحمل ويعرض البريد الوارد.
         * @param {string} searchQuery - استعلام البحث (اختياري).
         */
        async function loadIncomingMail(searchQuery = '') {
            if (!isAuthReady || !userId) return;

            let q = query(collection(db, getUserCollectionPath('incomingMail')));

            // تصفية البحث
            if (searchQuery) {
                // ملاحظة: لا يمكن استخدام 'where' مع 'orderBy' بدون فهرسة في Firestore
                // لذلك، سنقوم بالتصفية بعد جلب البيانات إذا كان هناك بحث نصي
            }

            try {
                const snapshot = await getDocs(q);
                incomingMailTableBody.innerHTML = '';
                let filteredDocs = [];

                snapshot.forEach((doc) => {
                    const data = doc.data();
                    // تطبيق التصفية اليدوية
                    if (searchQuery) {
                        const searchLower = searchQuery.toLowerCase();
                        const matches = [
                            data.letterNumber,
                            data.letterDate,
                            data.subject,
                            data.sender
                        ].some(field => field && String(field).toLowerCase().includes(searchLower));
                        if (matches) {
                            filteredDocs.push({ id: doc.id, data: data });
                        }
                    } else {
                        filteredDocs.push({ id: doc.id, data: data });
                    }
                });

                // عرض الوثائق المفلترة
                filteredDocs.forEach(({ id, data }) => {
                    const row = incomingMailTableBody.insertRow();
                    row.insertCell().textContent = data.letterNumber;
                    row.insertCell().textContent = data.letterDate;
                    row.insertCell().textContent = data.sender;
                    row.insertCell().textContent = data.gov;
                    row.insertCell().textContent = data.subject;
                    row.insertCell().textContent = data.followupStatus || '';
                    row.insertCell().textContent = data.notes || '';

                    const actionsCell = row.insertCell();
                    const editButton = document.createElement('button');
                    editButton.textContent = 'تعديل';
                    editButton.className = 'btn btn-secondary text-xs ml-2';
                    editButton.onclick = () => editIncomingMail(id, data);
                    actionsCell.appendChild(editButton);

                    const deleteButton = document.createElement('button');
                    deleteButton.textContent = 'حذف';
                    deleteButton.className = 'btn btn-danger text-xs';
                    deleteButton.onclick = () => deleteDocument('incomingMail', id);
                    actionsCell.appendChild(deleteButton);
                });
            } catch (error) {
                console.error("خطأ في تحميل البريد الوارد:", error);
                showMessage('خطأ في تحميل البريد الوارد: ' + error.message, 'error');
            }
        }

        /**
         * يضيف كتاب وارد جديد.
         */
        document.getElementById('addIncomingMailForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            if (!userId) {
                showMessage('يرجى تسجيل الدخول لإضافة كتاب وارد.', 'info');
                return;
            }
            const letterNumber = document.getElementById('incomingMailLetterNumber').value;
            const letterDate = document.getElementById('incomingMailLetterDate').value;
            const sender = document.getElementById('incomingMailSender').value;
            const gov = document.getElementById('incomingMailGov').value;
            const subject = document.getElementById('incomingMailSubject').value;
            const followupStatus = document.getElementById('incomingMailFollowupStatus').value;
            const notes = document.getElementById('incomingMailNotes').value;

            try {
                await addDoc(collection(db, getUserCollectionPath('incomingMail')), {
                    letterNumber, letterDate, sender, gov, subject, followupStatus, notes,
                    createdAt: new Date()
                });
                showMessage('تمت إضافة الكتاب الوارد بنجاح!', 'success');
                e.target.reset();
            } catch (e) {
                console.error("خطأ في إضافة الكتاب الوارد:", e);
                showMessage('خطأ في إضافة الكتاب الوارد: ' + e.message, 'error');
            }
        });

        /**
         * يفتح نموذج تعديل البريد الوارد.
         * @param {string} id - معرف الوثيقة.
         * @param {object} data - بيانات البريد الوارد الحالية.
         */
        function editIncomingMail(id, data) {
            const form = document.getElementById('addIncomingMailForm');
            document.getElementById('incomingMailLetterNumber').value = data.letterNumber;
            document.getElementById('incomingMailLetterDate').value = data.letterDate;
            document.getElementById('incomingMailSender').value = data.sender;
            document.getElementById('incomingMailGov').value = data.gov;
            document.getElementById('incomingMailSubject').value = data.subject;
            document.getElementById('incomingMailFollowupStatus').value = data.followupStatus || '';
            document.getElementById('incomingMailNotes').value = data.notes || '';

            const submitButton = form.querySelector('button[type="submit"]');
            submitButton.textContent = 'تحديث الكتاب الوارد';
            submitButton.onclick = async (e) => {
                e.preventDefault();
                try {
                    await updateDoc(getUserDocRef('incomingMail', id), {
                        letterNumber: document.getElementById('incomingMailLetterNumber').value,
                        letterDate: document.getElementById('incomingMailLetterDate').value,
                        sender: document.getElementById('incomingMailSender').value,
                        gov: document.getElementById('incomingMailGov').value,
                        subject: document.getElementById('incomingMailSubject').value,
                        followupStatus: document.getElementById('incomingMailFollowupStatus').value,
                        notes: document.getElementById('incomingMailNotes').value
                    });
                    showMessage('تم تحديث الكتاب الوارد بنجاح!', 'success');
                    form.reset();
                    submitButton.textContent = 'إضافة كتاب وارد';
                    submitButton.onclick = null;
                } catch (e) {
                    console.error("خطأ في تحديث الكتاب الوارد:", e);
                    showMessage('خطأ في تحديث الكتاب الوارد: ' + e.message, 'error');
                }
            };
        }

        /**
         * يتعامل مع زر البحث عن البريد الوارد.
         */
        document.getElementById('searchIncomingMailBtn').addEventListener('click', () => {
            const query = document.getElementById('incomingMailSearchQuery').value;
            loadIncomingMail(query);
        });

        // --- وظائف إدارة البريد الصادر ---

        /**
         * يحمل ويعرض البريد الصادر.
         * @param {string} searchQuery - استعلام البحث (اختياري).
         */
        async function loadOutgoingMail(searchQuery = '') {
            if (!isAuthReady || !userId) return;

            let q = query(collection(db, getUserCollectionPath('outgoingMail')));

            try {
                const snapshot = await getDocs(q);
                outgoingMailTableBody.innerHTML = '';
                let filteredDocs = [];

                snapshot.forEach((doc) => {
                    const data = doc.data();
                    // تطبيق التصفية اليدوية
                    if (searchQuery) {
                        const searchLower = searchQuery.toLowerCase();
                        const matches = [
                            data.letterNumber,
                            data.letterDate,
                            data.subject,
                            data.recipient
                        ].some(field => field && String(field).toLowerCase().includes(searchLower));
                        if (matches) {
                            filteredDocs.push({ id: doc.id, data: data });
                        }
                    } else {
                        filteredDocs.push({ id: doc.id, data: data });
                    }
                });

                // عرض الوثائق المفلترة
                filteredDocs.forEach(({ id, data }) => {
                    const row = outgoingMailTableBody.insertRow();
                    row.insertCell().textContent = data.letterNumber;
                    row.insertCell().textContent = data.letterDate;
                    row.insertCell().textContent = data.recipient;
                    row.insertCell().textContent = data.gov;
                    row.insertCell().textContent = data.subject;
                    row.insertCell().textContent = data.followupStatus || '';
                    row.insertCell().textContent = data.notes || '';

                    const actionsCell = row.insertCell();
                    const editButton = document.createElement('button');
                    editButton.textContent = 'تعديل';
                    editButton.className = 'btn btn-secondary text-xs ml-2';
                    editButton.onclick = () => editOutgoingMail(id, data);
                    actionsCell.appendChild(editButton);

                    const deleteButton = document.createElement('button');
                    deleteButton.textContent = 'حذف';
                    deleteButton.className = 'btn btn-danger text-xs';
                    deleteButton.onclick = () => deleteDocument('outgoingMail', id);
                    actionsCell.appendChild(deleteButton);
                });
            } catch (error) {
                console.error("خطأ في تحميل البريد الصادر:", error);
                showMessage('خطأ في تحميل البريد الصادر: ' + error.message, 'error');
            }
        }

        /**
         * يضيف كتاب صادر جديد.
         */
        document.getElementById('addOutgoingMailForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            if (!userId) {
                showMessage('يرجى تسجيل الدخول لإضافة كتاب صادر.', 'info');
                return;
            }
            const letterNumber = document.getElementById('outgoingMailLetterNumber').value;
            const letterDate = document.getElementById('outgoingMailLetterDate').value;
            const recipient = document.getElementById('outgoingMailRecipient').value;
            const gov = document.getElementById('outgoingMailGov').value;
            const subject = document.getElementById('outgoingMailSubject').value;
            const followupStatus = document.getElementById('outgoingMailFollowupStatus').value;
            const notes = document.getElementById('outgoingMailNotes').value;

            try {
                await addDoc(collection(db, getUserCollectionPath('outgoingMail')), {
                    letterNumber, letterDate, recipient, gov, subject, followupStatus, notes,
                    createdAt: new Date()
                });
                showMessage('تمت إضافة الكتاب الصادر بنجاح!', 'success');
                e.target.reset();
            } catch (e) {
                console.error("خطأ في إضافة الكتاب الصادر:", e);
                showMessage('خطأ في إضافة الكتاب الصادر: ' + e.message, 'error');
            }
        });

        /**
         * يفتح نموذج تعديل البريد الصادر.
         * @param {string} id - معرف الوثيقة.
         * @param {object} data - بيانات البريد الصادر الحالية.
         */
        function editOutgoingMail(id, data) {
            const form = document.getElementById('addOutgoingMailForm');
            document.getElementById('outgoingMailLetterNumber').value = data.letterNumber;
            document.getElementById('outgoingMailLetterDate').value = data.letterDate;
            document.getElementById('outgoingMailRecipient').value = data.recipient;
            document.getElementById('outgoingMailGov').value = data.gov;
            document.getElementById('outgoingMailSubject').value = data.subject;
            document.getElementById('outgoingMailFollowupStatus').value = data.followupStatus || '';
            document.getElementById('outgoingMailNotes').value = data.notes || '';

            const submitButton = form.querySelector('button[type="submit"]');
            submitButton.textContent = 'تحديث الكتاب الصادر';
            submitButton.onclick = async (e) => {
                e.preventDefault();
                try {
                    await updateDoc(getUserDocRef('outgoingMail', id), {
                        letterNumber: document.getElementById('outgoingMailLetterNumber').value,
                        letterDate: document.getElementById('outgoingMailLetterDate').value,
                        recipient: document.getElementById('outgoingMailRecipient').value,
                        gov: document.getElementById('outgoingMailGov').value,
                        subject: document.getElementById('outgoingMailLetterNumber').value,
                        followupStatus: document.getElementById('outgoingMailFollowupStatus').value,
                        notes: document.getElementById('outgoingMailNotes').value
                    });
                    showMessage('تم تحديث الكتاب الصادر بنجاح!', 'success');
                    form.reset();
                    submitButton.textContent = 'إضافة كتاب صادر';
                    submitButton.onclick = null;
                } catch (e) {
                    console.error("خطأ في تحديث الكتاب الصادر:", e);
                    showMessage('خطأ في تحديث الكتاب الصادر: ' + e.message, 'error');
                }
            };
        }

        /**
         * يتعامل مع زر البحث عن البريد الصادر.
         */
        document.getElementById('searchOutgoingMailBtn').addEventListener('click', () => {
            const query = document.getElementById('outgoingMailSearchQuery').value;
            loadOutgoingMail(query);
        });

        // --- وظيفة حذف عامة ---

        /**
         * يحذف وثيقة من مجموعة معينة.
         * @param {string} collectionName - اسم المجموعة.
         * @param {string} docId - معرف الوثيقة المراد حذفها.
         */
        async function deleteDocument(collectionName, docId) {
            if (!userId) {
                showMessage('يرجى تسجيل الدخول للحذف.', 'info');
                return;
            }
            if (confirm('هل أنت متأكد أنك تريد حذف هذا السجل؟')) { // استخدام confirm مؤقتًا، يفضل استبداله بمربع حوار مخصص
                try {
                    await deleteDoc(getUserDocRef(collectionName, docId));
                    showMessage('تم حذف السجل بنجاح!', 'success');
                } catch (e) {
                    console.error(`خطأ في حذف السجل من ${collectionName}:`, e);
                    showMessage(`خطأ في حذف السجل: ${e.message}`, 'error');
                }
            }
        }
    </script>
</body>
</html>
# b.m.n.raed
