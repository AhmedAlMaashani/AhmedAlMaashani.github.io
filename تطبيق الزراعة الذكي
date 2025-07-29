<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <meta name="theme-color" content="#27ae60">
  <title>زراعتي - تطبيق الزراعة الذكي</title>
  <link rel="manifest" href="manifest.json">
  <link rel="icon" type="image/png" href="icons/icon-192.png">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/FileSaver.js/2.0.5/FileSaver.min.js"></script>
  <style>
    * {
      box-sizing: border-box;
      font-family: 'Segoe UI', Arial, sans-serif;
    }
    body {
      margin: 0;
      padding: 20px;
      background-color: #f4f8f7;
      color: #2c3e50;
      direction: rtl;
      text-align: right;
    }
    h1, h2 {
      color: #27ae60;
    }
    .container {
      max-width: 900px;
      margin: 0 auto;
      background: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }
    .search-box {
      width: 100%;
      padding: 12px;
      font-size: 16px;
      border: 1px solid #bdc3c7;
      border-radius: 8px;
      margin-bottom: 20px;
    }
    .btn {
      background-color: #27ae60;
      color: white;
      border: none;
      padding: 12px 20px;
      font-size: 16px;
      border-radius: 8px;
      cursor: pointer;
      margin: 10px 0;
    }
    .btn:hover {
      background-color: #219653;
    }
    .crop-card {
      border: 1px solid #ecf0f1;
      border-radius: 10px;
      padding: 15px;
      margin-bottom: 15px;
      background: #f9fafa;
      cursor: pointer;
      transition: transform 0.2s;
    }
    .crop-card:hover {
      transform: translateY(-3px);
      box-shadow: 0 6px 12px rgba(0,0,0,0.1);
    }
    .crop-image {
      width: 80px;
      height: 80px;
      object-fit: cover;
      border-radius: 8px;
      float: right;
      margin-left: 15px;
    }
    .form-group {
      margin-bottom: 15px;
    }
    .form-group label {
      display: block;
      margin-bottom: 5px;
      font-weight: bold;
    }
    .form-group input, .form-group textarea {
      width: 100%;
      padding: 10px;
      border: 1px solid #bdc3c7;
      border-radius: 6px;
      font-size: 16px;
    }
    .modal {
      display: none;
      position: fixed;
      z-index: 1000;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0,0.5);
    }
    .modal-content {
      background-color: white;
      margin: 5% auto;
      padding: 20px;
      border-radius: 12px;
      width: 90%;
      max-width: 500px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.3);
    }
    .close {
      float: left;
      font-size: 28px;
      font-weight: bold;
      color: #aaa;
      cursor: pointer;
    }
    .close:hover {
      color: #000;
    }
    .crop-detail {
      background: #f8f9fa;
      padding: 20px;
      border-radius: 10px;
      margin-bottom: 15px;
    }
    .detail-row {
      display: flex;
      margin-bottom: 10px;
    }
    .detail-label {
      font-weight: bold;
      color: #27ae60;
      min-width: 120px;
    }
    .copy-btn {
      background-color: #3498db;
      color: white;
      border: none;
      padding: 8px 12px;
      border-radius: 6px;
      font-size: 14px;
      cursor: pointer;
      margin-top: 10px;
    }
    .copy-btn:hover {
      background-color: #2980b9;
    }
  </style>
</head>
<body>

  <div class="container">
    <h1>زراعتي 🌱</h1>
    <p>تطبيق الزراعة الذكي لإدارة المحاصيل</p>

    <input type="text" id="searchInput" class="search-box" placeholder="ابحث عن محصول..." />

    <button id="addCropBtn" class="btn">➕ إضافة محصول</button>

    <div id="cropsList"></div>
  </div>

  <!-- نافذة إضافة محصول -->
  <div id="addCropModal" class="modal">
    <div class="modal-content">
      <span class="close">&times;</span>
      <h2>إضافة محصول جديد</h2>
      <form id="cropForm">
        <div class="form-group">
          <label>اختر صورة</label>
          <input type="file" id="cropImage" accept="image/*" />
          <img id="preview" src="" alt="معاينة الصورة" style="max-width: 100%; margin-top: 10px; display: none;" />
        </div>
        <div class="form-group">
          <label>الاسم المحلي *</label>
          <input type="text" id="localName" required />
        </div>
        <div class="form-group">
          <label>الاسم العلمي</label>
          <input type="text" id="scientificName" />
        </div>
        <div class="form-group">
          <label>فترة التزهير</label>
          <input type="text" id="floweringPeriod" />
        </div>
        <div class="form-group">
          <label>فترة الثمار</label>
          <input type="text" id="fruitingPeriod" />
        </div>
        <div class="form-group">
          <label>عائلة النبتة</label>
          <input type="text" id="family" />
        </div>
        <div class="form-group">
          <label>عمر النبتة</label>
          <input type="text" id="lifespan" />
        </div>
        <div class="form-group">
          <label>الموقع</label>
          <input type="text" id="location" />
        </div>
        <div class="form-group">
          <label>احتياج التسميد</label>
          <textarea id="fertilizationNeeds" rows="3"></textarea>
        </div>
        <button type="submit" class="btn">حفظ المحصول</button>
      </form>
    </div>
  </div>

  <!-- نافذة التفاصيل -->
  <div id="detailModal" class="modal">
    <div class="modal-content">
      <span class="close-detail">&times;</span>
      <h2 id="detailTitle">تفاصيل المحصول</h2>
      <div id="detailContent" class="crop-detail"></div>
      <button id="copyToClipboard" class="copy-btn">📋 نسخ التفاصيل</button>
      <button id="downloadPdfBtn" class="btn">تنزيل كـ PDF</button>
    </div>
  </div>

  <script>
    // تفعيل Service Worker
    if ('serviceWorker' in navigator) {
      window.addEventListener('load', () => {
        navigator.serviceWorker.register('service-worker.js')
          .then(reg => console.log('SW مسجل', reg))
          .catch(err => console.log('خطأ في تسجيل SW', err));
      });
    }

    // المتغيرات
    let crops = JSON.parse(localStorage.getItem('crops') || '[]');
    const searchInput = document.getElementById('searchInput');
    const cropsList = document.getElementById('cropsList');
    const addCropBtn = document.getElementById('addCropBtn');
    const addCropModal = document.getElementById('addCropModal');
    const detailModal = document.getElementById('detailModal');
    const cropForm = document.getElementById('cropForm');
    const preview = document.getElementById('preview');
    const cropImage = document.getElementById('cropImage');

    // عرض الصورة
    cropImage.addEventListener('change', (e) => {
      const file = e.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = () => {
          preview.src = reader.result;
          preview.style.display = 'block';
        };
        reader.readAsDataURL(file);
      }
    });

    // فتح/إغلاق النافذات
    addCropBtn.onclick = () => {
      addCropModal.style.display = 'block';
      cropForm.reset();
      preview.style.display = 'none';
    };

    document.querySelector('.close').onclick = () => {
      addCropModal.style.display = 'none';
    };
    document.querySelector('.close-detail').onclick = () => {
      detailModal.style.display = 'none';
    };
    window.onclick = (e) => {
      if (e.target === addCropModal) addCropModal.style.display = 'none';
      if (e.target === detailModal) detailModal.style.display = 'none';
    };

    // حفظ المحصول
    cropForm.addEventListener('submit', async (e) => {
      e.preventDefault();
      const file = cropImage.files[0];
      let imageUrl = '';
      if (file) {
        imageUrl = await toBase64(file);
      }

      const newCrop = {
        id: Date.now().toString(),
        image: imageUrl,
        localName: document.getElementById('localName').value,
        scientificName: document.getElementById('scientificName').value,
        floweringPeriod: document.getElementById('floweringPeriod').value,
        fruitingPeriod: document.getElementById('fruitingPeriod').value,
        family: document.getElementById('family').value,
        lifespan: document.getElementById('lifespan').value,
        location: document.getElementById('location').value,
        fertilizationNeeds: document.getElementById('fertilizationNeeds').value,
      };

      crops.push(newCrop);
      localStorage.setItem('crops', JSON.stringify(crops));
      addCropModal.style.display = 'none';
      renderCrops();
      alert('تم حفظ المحصول بنجاح!');
    });

    // عرض المحاصيل
    function renderCrops(query = '') {
      const term = searchInput.value.toLowerCase();
      cropsList.innerHTML = '';
      const filtered = crops.filter(crop =>
        crop.localName.toLowerCase().includes(term) ||
        (crop.scientificName && crop.scientificName.toLowerCase().includes(term))
      );

      if (filtered.length === 0) {
        cropsList.innerHTML = '<p>لا توجد محاصيل. أضف واحدًا!</p>';
        return;
      }

      filtered.forEach(crop => {
        const div = document.createElement('div');
        div.className = 'crop-card';
        div.innerHTML = `
          <img src="${crop.image || 'https://via.placeholder.com/80'}" alt="صورة المحصول" class="crop-image" />
          <strong>${crop.localName}</strong><br>
          <small>${crop.scientificName || 'لا يوجد اسم علمي'}</small>
        `;
        div.onclick = () => showCropDetail(crop);
        cropsList.appendChild(div);
      });
    }

    // عرض التفاصيل
    function showCropDetail(crop) {
      const detailContent = document.getElementById('detailContent');
      detailContent.innerHTML = `
        ${crop.image ? `<img src="${crop.image}" alt="صورة المحصول" style="width:100%; height:120px; object-fit:cover; border-radius:8px; margin-bottom:15px;" />` : ''}
        <div class="detail-row"><div class="detail-label">الاسم المحلي:</div> <div>${crop.localName}</div></div>
        <div class="detail-row"><div class="detail-label">الاسم العلمي:</div> <div>${crop.scientificName || 'غير محدد'}</div></div>
        <div class="detail-row"><div class="detail-label">فترة التزهير:</div> <div>${crop.floweringPeriod || 'غير محدد'}</div></div>
        <div class="detail-row"><div class="detail-label">فترة الثمار:</div> <div>${crop.fruitingPeriod || 'غير محدد'}</div></div>
        <div class="detail-row"><div class="detail-label">عائلة النبتة:</div> <div>${crop.family || 'غير محدد'}</div></div>
        <div class="detail-row"><div class="detail-label">عمر النبتة:</div> <div>${crop.lifespan || 'غير محدد'}</div></div>
        <div class="detail-row"><div class="detail-label">الموقع:</div> <div>${crop.location || 'غير محدد'}</div></div>
        <div class="detail-row"><div class="detail-label">احتياج التسميد:</div> <div>${crop.fertilizationNeeds || 'غير محدد'}</div></div>
      `;
      document.getElementById('detailTitle').textContent = crop.localName;
      detailModal.style.display = 'block';
    }

    // تحويل الصورة إلى Base64
    function toBase64(file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.readAsDataURL(file);
        reader.onload = () => resolve(reader.result);
        reader.onerror = error => reject(error);
      });
    }

    // نسخ التفاصيل إلى الحافظة
    document.getElementById('copyToClipboard').addEventListener('click', () => {
      const text = document.getElementById('detailContent').innerText;
      navigator.clipboard.writeText(text).then(() => {
        alert('تم نسخ التفاصيل إلى الحافظة!');
      }).catch(err => {
        alert('فشل النسخ: ' + err);
      });
    });

    // تنزيل كـ PDF
    document.getElementById('downloadPdfBtn').addEventListener('click', async () => {
      const { jsPDF } = window.jspdf;
      const doc = new jsPDF();

      const crop = crops.find(c => c.localName === document.getElementById('detailTitle').textContent);
      doc.setFontSize(22);
      doc.text(crop.localName, 105, 20, null, null, 'center');

      if (crop.image) {
        const img = new Image();
        img.src = crop.image;
        await new Promise(resolve => { img.onload = resolve; });
        doc.addImage(img, 'JPEG', 15, 30, 180, 100);
      }

      let y = crop.image ? 140 : 30;
      doc.setFontSize(12);
      const fields = [
        ['الاسم المحلي', crop.localName],
        ['الاسم العلمي', crop.scientificName || 'غير محدد'],
        ['فترة التزهير', crop.floweringPeriod || 'غير محدد'],
        ['فترة الثمار', crop.fruitingPeriod || 'غير محدد'],
        ['عائلة النبتة', crop.family || 'غير محدد'],
        ['عمر النبتة', crop.lifespan || 'غير محدد'],
        ['الموقع', crop.location || 'غير محدد'],
        ['احتياج التسميد', crop.fertilizationNeeds || 'غير محدد'],
      ];

      fields.forEach(([label, value]) => {
        if (y > 280) {
          doc.addPage();
          y = 20;
        }
        doc.setFont('bold');
        doc.text(`${label}:`, 190, y, { align: 'right' });
        doc.setFont('normal');
        doc.text(value, 188, y + 5, { align: 'right' });
        y += 15;
      });

      doc.save(`${crop.localName}.pdf`);
    });

    // بحث
    searchInput.addEventListener('input', renderCrops);

    // تحميل المحاصيل
    renderCrops();
  </script>
</body>
</html>
