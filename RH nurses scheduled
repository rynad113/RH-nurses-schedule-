<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <title>تنظيم الجدول الدراسي - كلية التمريض</title>
  <style>
    body {
      font-family: 'Cairo', sans-serif;
      direction: rtl;
      padding: 20px;
      background: #f5f5f5;
    }
    label, select, input, button {
      display: block;
      margin: 10px 0;
      font-size: 18px;
    }
    select, input {
      padding: 8px;
      width: 100%;
    }
    .course-section {
      border: 1px solid #ccc;
      background: #fff;
      padding: 15px;
      margin-bottom: 15px;
      font-size: 18px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
      background: #fff;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 10px;
      text-align: center;
    }
    #printBtn {
      margin-top: 20px;
      font-size: 20px;
      background-color: #4CAF50;
      color: white;
      padding: 10px 20px;
      border: none;
      cursor: pointer;
    }
    @media print {
      body * {
        visibility: hidden;
      }
      #schedule, #schedule * {
        visibility: visible;
      }
      #schedule {
        position: absolute;
        top: 0;
        right: 0;
        left: 0;
      }
    }
  </style>
</head>
<body>
  <h2>تنظيم الجدول الدراسي - كلية التمريض</h2>

  <label for="level">اختر المستوى الدراسي:</label>
  <select id="level" onchange="showCourses()">
    <option value="">-- اختر --</option>
    <option value="3">المستوى الثالث</option>
    <option value="4">المستوى الرابع</option>
    <option value="5">المستوى الخامس</option>
    <option value="6">المستوى السادس</option>
    <option value="7">المستوى السابع</option>
  </select>

  <label for="off-day">اختر يوم الإجازة المفضل (اختياري):</label>
  <select id="off-day">
    <option value="">بدون</option>
    <option value="الأحد">الأحد</option>
    <option value="الاثنين">الاثنين</option>
    <option value="الثلاثاء">الثلاثاء</option>
    <option value="الأربعاء">الأربعاء</option>
    <option value="الخميس">الخميس</option>
  </select>

  <div id="courses"></div>

  <button onclick="generateSchedule()">تنظيم الجدول</button>

  <div id="schedule"></div>
  <button id="printBtn" onclick="window.print()">طباعة الجدول</button>

  <script>
    const coursesByLevel = {
      3: [
        { code: 'ANT-214', name: 'علم التشريح', units: 3 },
        { code: 'BOCH-215', name: 'الكيمياء الحيوية', units: 2 },
        { code: 'NUR-211', name: 'أساسيات التمريض نظري', units: 3 },
        { code: 'NUR-212', name: 'أساسيات التمريض عملي', units: 3 },
        { code: 'NUR-213', name: 'التقييم الصحي نظري', units: 2 },
        { code: 'NUR-214', name: 'التقييم الصحي عملي', units: 2 },
        { code: 'PHYL-213', name: 'علم وظائف الأعضاء', units: 3 }
      ],
      4: [
        { code: 'MIBO-227', name: 'علم الأحياء الدقيقة', units: 2 },
        { code: 'NUR-225', name: 'تمريض صحة البالغين 1 نظري', units: 4 },
        { code: 'NUR-226', name: 'تمريض صحة البالغين 1 عملي', units: 6 },
        { code: 'PATH-228', name: 'الفيسيولوجيا المرضية', units: 2 },
        { code: 'PHRM-226', name: 'علم الأدوية للتمريض', units: 3 }
      ],
      5: [
        { code: 'NUR-425', name: 'رعاية الحالات الحادة نظري', units: 4 },
        { code: 'NUR-426', name: 'رعاية الحالات الحادة عملي', units: 3 },
        { code: 'NUR-427', name: 'تمريض صحة المجتمع نظري', units: 3 },
        { code: 'NUR-428', name: 'تمريض صحة المجتمع عملي', units: 3 }
      ],
      6: [
        { code: 'NUR-325', name: 'تمريض الأطفال نظري', units: 3 },
        { code: 'NUR-326', name: 'تمريض الأطفال عملي', units: 3 },
        { code: 'NUR-327', name: 'النمو والتطور', units: 2 },
        { code: 'NUR-328', name: 'مقدمة في أبحاث التمريض', units: 3 },
        { code: 'NUTR-323', name: 'التغذية البشرية', units: 2 },
        { code: 'SOCI-324', name: 'علم الاجتماع للتمريض', units: 1 }
      ],
      7: [
        { code: 'NUR-411', name: 'تمريض الصحة النفسية - نظري', units: 3 },
        { code: 'NUR-412', name: 'تمريض الصحة النفسية - عملي', units: 3 },
        { code: 'NUR-413', name: 'القضايا القانونية والأخلاقية في التمريض', units: 2 },
        { code: 'NUR-414', name: 'القيادة والأدارة في التمريض', units: 2 },
        { code: 'NUR-415', name: 'التثقيف والأرتقاء الصحي', units: 2 },
        { code: 'NUR-416', name: 'المعلوماتية الصحية', units: 2 },
        { code: 'NUR-425', name: 'تمريض رعاية الحالات الحاده والمعقده - نظري', units: 4 },
        { code: 'NUR-426', name: 'تمريض رعاية الحالات الحاده والمعقده - عملي', units: 3 },
        { code: 'NUR-427', name: 'تمريض صحة المجتمع - نظري', units: 3 },
        { code: 'NUR-428', name: 'تمريض صحة المجتمع - عملي', units: 3 }
      ]
    };

    function showCourses() {
      const level = document.getElementById('level').value;
      const courseDiv = document.getElementById('courses');
      courseDiv.innerHTML = '';
      if (!level || !coursesByLevel[level]) return;
      coursesByLevel[level].forEach(course => {
        const courseSection = document.createElement('div');
        courseSection.className = 'course-section';
        courseSection.innerHTML = `
          <strong>${course.code} - ${course.name}</strong> (${course.units} ساعات)<br>
          <label>أدخل معلومات الشعبة (اليوم + الوقت):</label>
          <input type="text" class="section-time" placeholder="مثال: الأحد 8:00-9:30">
        `;
        courseDiv.appendChild(courseSection);
      });
    }

    function generateSchedule() {
      const inputs = document.querySelectorAll('.course-section');
      const scheduleData = [];
      const conflicts = [];
      const usedSlots = new Set();

      inputs.forEach(section => {
        const title = section.querySelector('strong').innerText;
        const timeInput = section.querySelector('input').value.trim();
        if (!timeInput) return;

        const slotKey = timeInput.replaceAll(' ', '');
        if (usedSlots.has(slotKey)) {
          conflicts.push(`${title} يتعارض مع مقرر آخر في نفس الوقت: ${timeInput}`);
        } else {
          usedSlots.add(slotKey);
          scheduleData.push({ title, time: timeInput });
        }
      });

      const scheduleDiv = document.getElementById('schedule');
      scheduleDiv.innerHTML = '';

      if (conflicts.length > 0) {
        const alertBox = document.createElement('div');
        alertBox.style.color = 'red';
        alertBox.style.marginTop = '20px';
        alertBox.innerHTML = '<strong>التعارضات:</strong><ul>' + conflicts.map(c => `<li>${c}</li>`).join('') + '</ul>';
        scheduleDiv.appendChild(alertBox);
      }

      if (scheduleData.length > 0) {
        const table = document.createElement('table');
        table.id = 'schedule-table';
        table.innerHTML = `
          <thead>
            <tr>
              <th>المقرر</th>
              <th>اليوم والوقت</th>
            </tr>
          </thead>
          <tbody>
            ${scheduleData.map(row => `<tr><td>${row.title}</td><td>${row.time}</td></tr>`).join('')}
          </tbody>
        `;
        scheduleDiv.appendChild(table);
      }
    }
  </script>
</body>
</html>
