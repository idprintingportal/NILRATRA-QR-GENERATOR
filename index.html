<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shiv Nirmal ITI - Smart Result & Clean Barcode Card Generator</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- QR Code Library -->
    <script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.1/build/qrcode.min.js"></script>
    <!-- html2canvas for card image export -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <!-- FileSaver Library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/FileSaver.js/2.0.5/FileSaver.min.js"></script>
    <!-- Tesseract.js for OCR Image Recognition -->
    <script src="https://cdn.jsdelivr.net/npm/tesseract.js@5/dist/tesseract.min.js"></script>
    <style>
        /* Custom Styling for Movable and Resizable Barcode / QR Code Box */
        #qrMovableContainer {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 120px;
            height: 120px;
            min-width: 50px;
            min-height: 50px;
            cursor: move;
            user-select: none;
            touch-action: none;
            z-index: 30;
            box-sizing: border-box;
        }
        /* 4 Corner Resize Handles */
        .resize-handle {
            position: absolute;
            width: 16px;
            height: 16px;
            background: #0284c7;
            border: 2px solid #fff;
            border-radius: 3px;
            z-index: 40;
            touch-action: none;
            box-shadow: 0 1px 4px #0009;
        }
        .handle-tl { top: -5px; left: -5px; cursor: nwse-resize; }
        .handle-tr { top: -5px; right: -5px; cursor: nesw-resize; }
        .handle-bl { bottom: -5px; left: -5px; cursor: nesw-resize; }
        .handle-br { bottom: -5px; right: -5px; cursor: nwse-resize; }
    </style>
</head>
<body class="bg-slate-900 text-slate-100 min-h-screen">

    <!-- Header -->
    <header class="bg-slate-800 border-b border-slate-700 py-4 px-6 shadow-md">
        <div class="max-w-[96%] mx-auto flex flex-col md:flex-row justify-between items-center gap-4">
            <div>
                <h1 class="text-xl font-bold text-amber-400 flex items-center gap-2">
                    ⚡ Shiv Nirmal ITI - Clean Image & Barcode Generator
                </h1>
                <p class="text-xs text-slate-400">Upload background image, place movable/resizable QR Barcode on top, and download clean image</p>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="max-w-[96%] mx-auto p-4 md:p-6 grid grid-cols-1 lg:grid-cols-12 gap-6">
        
        <!-- Left Panel: Input Fields & Photo Uploads -->
        <section class="lg:col-span-5 bg-slate-800 border border-slate-700 rounded-xl p-5 shadow-lg flex flex-col gap-3">
            <h2 class="text-lg font-semibold text-sky-400 border-b border-slate-700 pb-2">📥 Input Data & Document Auto-Compress</h2>
            
            <!-- OCR Image Paste/Upload Box -->
            <div class="bg-slate-900 border-2 border-dashed border-sky-500/50 rounded-lg p-3 text-center cursor-pointer hover:border-sky-400 transition focus:outline-none" id="dropZone" tabindex="0">
                <p class="text-xs font-bold text-sky-300">📋 Click here & Press Ctrl+V to Paste OCR Result Image</p>
                <p class="text-[10px] text-slate-400 mt-1">Or choose an OCR image file:</p>
                <input type="file" id="imageUpload" accept="image/*" class="mt-1 text-xs text-slate-300 file:mr-2 file:py-1 file:px-3 file:rounded file:border-0 file:text-xs file:font-semibold file:bg-sky-600 file:text-white hover:file:bg-sky-500">
                <p id="ocrStatus" class="text-[11px] text-amber-400 mt-1 font-semibold"></p>
            </div>

            <!-- 3 Document Upload Section with High-Quality Auto Compression -->
            <div class="bg-slate-900 border border-slate-700 rounded-lg p-3 flex flex-col gap-2">
                <p class="text-xs font-bold text-emerald-400 uppercase">📄 Upload 3 Documents (Auto-Compress):</p>
                
                <div class="grid grid-cols-3 gap-2">
                    <div>
                        <label class="block text-[10px] font-bold text-slate-300 uppercase mb-1">Doc 1:</label>
                        <input type="file" id="photo1Input" accept="image/*" onchange="processAndCompressDocument(this)" class="w-full text-[10px] text-slate-400 file:mr-1 file:py-0.5 file:px-2 file:rounded file:border-0 file:text-[10px] file:bg-emerald-600 file:text-white">
                    </div>
                    <div>
                        <label class="block text-[10px] font-bold text-slate-300 uppercase mb-1">Doc 2:</label>
                        <input type="file" id="photo2Input" accept="image/*" onchange="processAndCompressDocument(this)" class="w-full text-[10px] text-slate-400 file:mr-1 file:py-0.5 file:px-2 file:rounded file:border-0 file:text-[10px] file:bg-emerald-600 file:text-white">
                    </div>
                    <div>
                        <label class="block text-[10px] font-bold text-slate-300 uppercase mb-1">Doc 3:</label>
                        <input type="file" id="photo3Input" accept="image/*" onchange="processAndCompressDocument(this)" class="w-full text-[10px] text-slate-400 file:mr-1 file:py-0.5 file:px-2 file:rounded file:border-0 file:text-[10px] file:bg-emerald-600 file:text-white">
                    </div>
                </div>
            </div>

            <!-- Basic Info Fields -->
            <div class="grid grid-cols-2 gap-2">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Base URL:</label>
        <input type="text" id="baseUrl" value="https://nemrc.co.in/result.php" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Course:</label>
                    <input type="text" id="courseVal" value="ITI" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
            </div>

            <div class="grid grid-cols-2 gap-2">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Student Name:</label>
                    <input type="text" id="studentName" placeholder="e.g. Roshan Bistur sawara" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Seat Number:</label>
                    <input type="text" id="seatNo" placeholder="e.g. A1321789" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
            </div>

            <div class="grid grid-cols-2 gap-2">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Date Of Birth:</label>
                    <input type="text" id="dob" placeholder="YYYY-MM-DD" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Year:</label>
                    <input type="text" id="yearVal" placeholder="2023 to 2025" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
            </div>

            <div class="grid grid-cols-2 gap-2">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Trade:</label>
                    <input type="text" id="trade" placeholder="Electrician" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Practical Marks:</label>
                    <input type="text" id="practical" placeholder="331" oninput="calculateTotal()" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
            </div>

            <!-- Subject Marks Fields -->
            <div class="grid grid-cols-2 gap-2">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Theory Marks:</label>
                    <input type="text" id="theory" placeholder="89" oninput="calculateTotal()" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Workshop Calc & Sci:</label>
                    <input type="text" id="wcs" placeholder="52" oninput="calculateTotal()" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
            </div>

            <div class="grid grid-cols-2 gap-2">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Engineering Drawing:</label>
                    <input type="text" id="ed" placeholder="44" oninput="calculateTotal()" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Social Study:</label>
                    <input type="text" id="socialStudy" placeholder="41" oninput="calculateTotal()" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
            </div>

            <div class="grid grid-cols-2 gap-2">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Total Marks:</label>
                    <input type="text" id="totalMarks" placeholder="Auto-calculated" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none font-bold text-amber-400">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">OutOff Marks:</label>
                    <input type="text" id="cutoff" value="700" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
            </div>

            <button onclick="generateCardQR()" class="mt-2 w-full bg-blue-600 hover:bg-blue-500 text-white font-bold py-2.5 rounded-lg shadow text-xs">
                🚀 Generate Barcode / QR Code
            </button>
        </section>

        <!-- Right Panel: Image Upload & Barcode Only Preview -->
        <section class="lg:col-span-7 flex flex-col gap-6">
            <div class="bg-slate-800 border border-slate-700 rounded-xl p-5 shadow-lg">
                <div class="flex flex-wrap justify-between items-center border-b border-slate-700 pb-3 mb-4 gap-2">
                    <h2 class="text-lg font-semibold text-emerald-400">🖼️ Image & Barcode Preview</h2>
                    <div class="flex items-center gap-2">
                        <!-- Custom Preview Image Upload Button -->
                        <label class="bg-sky-600 hover:bg-sky-500 text-white text-xs font-bold px-3 py-2 rounded cursor-pointer transition flex items-center gap-1 shadow">
                            📁 Upload Background Image
                            <input type="file" id="cardBgUpload" accept="image/*" onchange="uploadCardBackground(this)" class="hidden">
                        </label>
                        <button onclick="downloadCardImage()" class="bg-emerald-600 hover:bg-emerald-500 text-white text-xs font-bold px-3 py-2 rounded transition shadow">
                            📥 Download Image
                        </button>
                    </div>
                </div>
                
                <!-- Pure Image Container for Barcode Overlay -->
                <div id="captureCard" class="bg-slate-950 rounded-lg border-2 border-slate-600 shadow-md flex items-center justify-center relative overflow-hidden min-h-[450px] w-full">
                    
                    <!-- Placeholder Text if no image is uploaded -->
                    <div id="noImgText" class="text-slate-500 text-sm font-medium text-center p-6">
                        🖼️ Upload background image using the top button.<br>Only uploaded image & barcode will be displayed and downloaded.
                    </div>

                    <!-- Uploaded Image Display -->
                    <img id="cardBgImg" class="w-full h-auto object-contain hidden relative z-0" alt="Card Background">

                    <!-- MOVABLE & RESIZABLE BARCODE / QR CODE CONTAINER -->
                    <div id="qrMovableContainer" class="bg-white p-1.5 border-2 border-dashed border-sky-500 rounded shadow-2xl flex items-center justify-center">
                        <canvas id="qrCanvas" class="w-full h-full object-contain"></canvas>
                        
                        <!-- 4 Corner Resize Handles -->
                        <div class="resize-handle handle-tl" data-handle="tl" title="Resize Top-Left"></div>
                        <div class="resize-handle handle-tr" data-handle="tr" title="Resize Top-Right"></div>
                        <div class="resize-handle handle-bl" data-handle="bl" title="Resize Bottom-Left"></div>
                        <div class="resize-handle handle-br" data-handle="br" title="Resize Bottom-Right"></div>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <script>
        // Compress Document Image
        function processAndCompressDocument(input) {
            const file = input.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function (e) {
                const img = new Image();
                img.src = e.target.result;

                img.onload = function () {
                    const canvas = document.createElement('canvas');
                    canvas.width = img.width > 800 ? 800 : img.width;
                    canvas.height = (img.height * canvas.width) / img.width;

                    const ctx = canvas.getContext('2d');
                    ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
                    canvas.toDataURL('image/jpeg', 0.80);
                };
            };
            reader.readAsDataURL(file);
        }

        // Upload Preview Background Image
        function uploadCardBackground(input) {
            const file = input.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function (e) {
                const bgImg = document.getElementById('cardBgImg');
                const noImgText = document.getElementById('noImgText');

                bgImg.src = e.target.result;
                bgImg.classList.remove('hidden');
                if (noImgText) noImgText.classList.add('hidden');
            };
            reader.readAsDataURL(file);
        }

        function calculateTotal() {
            const practical = parseFloat(document.getElementById('practical').value) || 0;
            const theory = parseFloat(document.getElementById('theory').value) || 0;
            const wcs = parseFloat(document.getElementById('wcs').value) || 0;
            const ed = parseFloat(document.getElementById('ed').value) || 0;
            const socialStudy = parseFloat(document.getElementById('socialStudy').value) || 0;

            const sum = practical + theory + wcs + ed + socialStudy;
            if (sum > 0) {
                document.getElementById('totalMarks').value = sum;
            }
        }

        function generateCardQR() {
            const baseUrl = document.getElementById('baseUrl').value.trim();
            const courseVal = document.getElementById('courseVal').value.trim();
            const seatNo = document.getElementById('seatNo').value.trim() || "N/A";
            const studentName = document.getElementById('studentName').value.trim() || "N/A";
            const dob = document.getElementById('dob').value.trim() || "N/A";
            const yearVal = document.getElementById('yearVal').value.trim() || "N/A";
            const trade = document.getElementById('trade').value.trim() || "N/A";
            const practical = document.getElementById('practical').value.trim() || "N/A";
            const theory = document.getElementById('theory').value.trim() || "N/A";
            const wcs = document.getElementById('wcs').value.trim() || "N/A";
            const ed = document.getElementById('ed').value.trim() || "N/A";
            const socialStudy = document.getElementById('socialStudy').value.trim() || "N/A";
            const totalMarks = document.getElementById('totalMarks').value.trim() || "N/A";
            const cutoff = document.getElementById('cutoff').value.trim() || "700";

            let targetUrl;
            try {
                const resultUrl = new URL(baseUrl);
                resultUrl.searchParams.set('course', courseVal);
                resultUrl.searchParams.set('seat', seatNo);
                targetUrl = resultUrl.toString();
            } catch (error) {
                console.error('Invalid result URL:', error);
                alert('Base URL sahi nahi hai. Kripya valid URL daalein.');
                return;
            }

            const qrPayload = `=========================\nSHIV NIRMAL ITI\n=========================\nStudent Name: ${studentName}\nSeat No: ${seatNo}\nDOB: ${dob}\nYear: ${yearVal}\nTrade: ${trade}\nPractical: ${practical}\nTheory: ${theory}\nWorkshop Calc & Sci: ${wcs}\nEngineering Drawing: ${ed}\nSocial Study: ${socialStudy}\nTotal: ${totalMarks} / ${cutoff}\n-------------------------\nOfficial Result Search Link:\n${targetUrl}`;

            const canvas = document.getElementById('qrCanvas');
            if (!window.QRCode || typeof QRCode.toCanvas !== 'function') {
                console.error('QR library is unavailable. Check the internet connection and reload.');
                alert('QR library load nahi hui. Internet connection check karke page reload karein.');
                return;
            }
            QRCode.toCanvas(canvas, qrPayload, { width: 300, margin: 1 }, function (error) {
                if (error) {
                    console.error('QR Generation Error:', error);
                    alert('QR code generate nahi hua. Input data check karke dobara try karein.');
                }
            });
        }

        // Export/Download Image with Barcode Overlay
        function downloadCardImage() {
            const cardElement = document.getElementById('captureCard');
            const qrContainer = document.getElementById('qrMovableContainer');
            const resizeHandles = document.querySelectorAll('.resize-handle');

            // Keep editing controls out of the exported image and always restore them.
            const previousBorder = qrContainer.style.border;
            qrContainer.style.border = 'none';
            resizeHandles.forEach(h => h.style.visibility = 'hidden');
            html2canvas(cardElement, { scale: 3, useCORS: true, backgroundColor: null })
                .then(canvas => new Promise((resolve, reject) => {
                    canvas.toBlob(blob => blob ? resolve(blob) : reject(new Error('Image export failed')), 'image/png');
                }))
                .then(blob => {
                    if (typeof saveAs === 'function') {
                        saveAs(blob, `Result_Barcode_Image_${document.getElementById('seatNo').value || 'Data'}.png`);
                    } else {
                        const link = document.createElement('a');
                        link.href = URL.createObjectURL(blob);
                        link.download = `Result_Barcode_Image_${document.getElementById('seatNo').value || 'Data'}.png`;
                        link.click();
                        URL.revokeObjectURL(link.href);
                    }
                })
                .catch(error => {
                    console.error('Image export error:', error);
                    alert('Image download nahi ho paya. Dobara try karein.');
                })
                .finally(() => {
                    qrContainer.style.border = previousBorder;
                    resizeHandles.forEach(h => h.style.visibility = '');
                });
        }

        // Pointer events support mouse, touch, and pen. The opposite corner stays fixed while resizing.
        const qrContainer = document.getElementById('qrMovableContainer');
        const cardParent = document.getElementById('captureCard');
        let interaction = null;

        function cardPoint(event) {
            const rect = cardParent.getBoundingClientRect();
            return {
                x: event.clientX - rect.left - cardParent.clientLeft,
                y: event.clientY - rect.top - cardParent.clientTop
            };
        }

        function clamp(value, min, max) {
            return Math.min(Math.max(value, min), max);
        }

        qrContainer.addEventListener('pointerdown', event => {
            if (event.button !== undefined && event.button !== 0) return;
            event.preventDefault();
            const handle = event.target.closest('.resize-handle');
            const point = cardPoint(event);
            const left = qrContainer.offsetLeft;
            const top = qrContainer.offsetTop;
            const size = qrContainer.getBoundingClientRect().width;
            interaction = {
                pointerId: event.pointerId,
                mode: handle ? 'resize' : 'drag',
                corner: handle?.dataset.handle,
                startX: point.x,
                startY: point.y,
                left,
                top,
                size
            };
            qrContainer.setPointerCapture(event.pointerId);
        });

        qrContainer.addEventListener('pointermove', event => {
            if (!interaction || event.pointerId !== interaction.pointerId) return;
            const point = cardPoint(event);
            const maxLeft = Math.max(0, cardParent.clientWidth - qrContainer.offsetWidth);
            const maxTop = Math.max(0, cardParent.clientHeight - qrContainer.offsetHeight);

            if (interaction.mode === 'drag') {
                const left = clamp(interaction.left + point.x - interaction.startX, 0, maxLeft);
                const top = clamp(interaction.top + point.y - interaction.startY, 0, maxTop);
                qrContainer.style.left = `${left}px`;
                qrContainer.style.top = `${top}px`;
                qrContainer.style.right = 'auto';
                return;
            }

            const corner = interaction.corner;
            const fixedX = corner.includes('l') ? interaction.left + interaction.size : interaction.left;
            const fixedY = corner.includes('t') ? interaction.top + interaction.size : interaction.top;
            const xSign = corner.includes('l') ? -1 : 1;
            const ySign = corner.includes('t') ? -1 : 1;
            const dx = (point.x - interaction.startX) * xSign;
            const dy = (point.y - interaction.startY) * ySign;
            const minSize = 50;
            const maxWidth = xSign < 0 ? fixedX : cardParent.clientWidth - fixedX;
            const maxHeight = ySign < 0 ? fixedY : cardParent.clientHeight - fixedY;
            const maxSize = Math.max(minSize, Math.min(maxWidth, maxHeight));
            const size = clamp(interaction.size + Math.max(dx, dy), minSize, maxSize);
            const left = xSign < 0 ? fixedX - size : fixedX;
            const top = ySign < 0 ? fixedY - size : fixedY;

            qrContainer.style.width = `${size}px`;
            qrContainer.style.height = `${size}px`;
            qrContainer.style.left = `${left}px`;
            qrContainer.style.top = `${top}px`;
            qrContainer.style.right = 'auto';
        });

        function endInteraction(event) {
            if (interaction && (!event || event.pointerId === interaction.pointerId)) interaction = null;
        }
        qrContainer.addEventListener('pointerup', endInteraction);
        qrContainer.addEventListener('pointercancel', endInteraction);
        qrContainer.addEventListener('lostpointercapture', endInteraction);

        // OCR Processing Handler
        const dropZone = document.getElementById('dropZone');
        const imageUpload = document.getElementById('imageUpload');
        const ocrStatus = document.getElementById('ocrStatus');

        dropZone.addEventListener('paste', function(e) {
            const items = e.clipboardData?.items;
            if (!items) return;
            for (let item of items) {
                if (item.type.indexOf('image') === 0) {
                    const blob = item.getAsFile();
                    processImage(blob);
                    break;
                }
            }
        });

        imageUpload.addEventListener('change', function(e) {
            if (e.target.files && e.target.files[0]) {
                processImage(e.target.files[0]);
            }
        });

        function processImage(file) {
            ocrStatus.innerText = "🔍 Reading image data via OCR...";
            Tesseract.recognize(
                file,
                'eng',
                { logger: m => console.log(m) }
            ).then(({ data: { text } }) => {
                ocrStatus.innerText = "✅ Data extracted & auto-filled successfully!";
                parseExtractedText(text);
            }).catch(err => {
                ocrStatus.innerText = "❌ Could not read image. Please try clear image.";
                console.error(err);
            });
        }

        function parseExtractedText(text) {
            const lines = text.split('\n').map(l => l.trim()).filter(l => l.length > 0);

            ['seatNo', 'studentName', 'dob', 'trade', 'practical', 'theory', 'wcs', 'ed', 'socialStudy', 'totalMarks'].forEach(id => {
                document.getElementById(id).value = "";
            });

            let foundSeat = "";
            let foundDates = [];

            for (let line of lines) {
                if (!foundSeat && /[A-Z]\d{6,10}/i.test(line)) {
                    const match = line.match(/[A-Z]\d{6,10}/i);
                    if (match) foundSeat = match[0];
                }
                if (/\d{4}[-/]\d{2}[-/]\d{2}/.test(line)) {
                    const match = line.match(/\d{4}[-/]\d{2}[-/]\d{2}/);
                    if (match) foundDates.push(match[0]);
                }
            }

            if (foundSeat) document.getElementById('seatNo').value = foundSeat;
            if (foundDates.length > 0) document.getElementById('dob').value = foundDates[0];

            if (lines.length > 0 && !/[A-Z]\d{6,10}/i.test(lines[0])) {
                document.getElementById('studentName').value = lines[0];
            }

            generateCardQR();
        }

        // Initialize empty QR canvas on load
        window.onload = function() {
            generateCardQR();
        };
    </script>
</body>
</html>
