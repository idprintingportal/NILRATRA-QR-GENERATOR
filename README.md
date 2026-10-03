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
        #scanResultPage { display: none; }
        body.result-view { background: #f8fafc; color: #1e293b; min-height: 100vh; }
        body.result-view > header, body.result-view > main { display: none; }
        body.result-view #scanResultPage { display: block; }
        .result-table th, .result-table td { border: 1px solid #d1d5db; padding: 12px 14px; text-align: left; vertical-align: top; }
        .result-table th { background: #f1f5f9; color: #334155; font-weight: 700; }
        .result-table td { background: white; color: #475569; overflow-wrap: anywhere; }
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
        #qrCanvas {
            width: 100%;
            height: 100%;
            object-fit: fill;
            flex: none;
            pointer-events: none;
            opacity: 1;
            background: transparent;
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

    <section id="scanResultPage" class="mx-auto max-w-7xl px-4 py-8 sm:px-6">
        <div class="overflow-hidden rounded-xl border border-slate-200 bg-white shadow-lg">
            <div class="border-b border-slate-200 px-6 py-5 text-center">
                <h1 class="text-2xl font-bold tracking-wide text-slate-800">Shiv Nirmal ITI</h1>
                <p class="mt-1 text-sm text-slate-500">Student Result</p>
            </div>
            <div class="overflow-x-auto">
                <table class="result-table w-full min-w-[1050px] border-collapse text-sm">
                    <thead><tr><th>Student Name</th><th>Seat No</th><th>Date Of Birth</th><th>Year</th><th>Trade</th><th>Practical Marks</th><th>Theory Marks</th><th>Workshop Calculation Science</th><th>Engineering Drawing</th><th>Social Study</th><th>Total Marks</th><th>OutOff Marks</th></tr></thead>
                    <tbody><tr id="scanResultRow"></tr></tbody>
                </table>
            </div>
        </div>
        <p class="mt-5 text-center text-sm"><a id="officialResultLink" class="break-all font-semibold text-blue-700 underline hover:text-blue-900" target="_blank" rel="noopener noreferrer">Open Official Result</a></p>
    </section>

    <!-- Main Container -->
    <main class="max-w-[96%] mx-auto p-4 md:p-6 grid grid-cols-1 lg:grid-cols-12 gap-6">
        
        <!-- Left Panel: Input Fields & Photo Uploads -->
        <section class="lg:col-span-5 bg-slate-800 border border-slate-700 rounded-xl p-5 shadow-lg flex flex-col gap-3">
            <h2 class="text-lg font-semibold text-sky-400 border-b border-slate-700 pb-2">📥 Result Image OCR & Auto Fill</h2>
            
            <!-- OCR Image Paste/Upload Box -->
            <div class="bg-slate-900 border-2 border-dashed border-sky-500/50 rounded-lg p-3 text-center cursor-pointer hover:border-sky-400 transition focus:outline-none" id="dropZone" tabindex="0">
                <p class="text-xs font-bold text-sky-300">🖼️ Upload or drop a result image here — fields will fill automatically</p>
                <p class="text-[10px] text-slate-400 mt-1">You can also paste a copied image with Ctrl+V.</p>
                <input type="file" id="imageUpload" accept="image/*" class="mt-2 text-xs text-slate-300 file:mr-2 file:py-1 file:px-3 file:rounded file:border-0 file:text-xs file:font-semibold file:bg-sky-600 file:text-white hover:file:bg-sky-500">
                <p id="ocrStatus" class="text-[11px] text-amber-400 mt-1 font-semibold"></p>
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
                    <div id="qrMovableContainer" class="bg-transparent p-0 border-0 rounded-none shadow-none flex items-center justify-center">
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

            const resultData = {
                name: studentName, seat: seatNo, dob, year: yearVal, trade,
                practical, theory, wcs, ed, socialStudy, total: totalMarks, cutoff,
                officialUrl: targetUrl
            };
            let qrPayload;
            if (location.protocol === 'http:' || location.protocol === 'https:') {
                const scanUrl = new URL(location.href);
                scanUrl.search = '';
                scanUrl.hash = '';
                scanUrl.searchParams.set('result', JSON.stringify(resultData));
                qrPayload = scanUrl.toString();
            } else {
                // Local file previews cannot provide a shareable formatted result page.
                qrPayload = `SHIV NIRMAL ITI\nStudent Name: ${studentName}\nSeat No: ${seatNo}\nDOB: ${dob}\nYear: ${yearVal}\nTrade: ${trade}\nPractical: ${practical}\nTheory: ${theory}\nWorkshop Calc & Sci: ${wcs}\nEngineering Drawing: ${ed}\nSocial Study: ${socialStudy}\nTotal: ${totalMarks} / ${cutoff}\nOfficial Result: ${targetUrl}`;
            }

            const canvas = document.getElementById('qrCanvas');
            if (!window.QRCode || typeof QRCode.toCanvas !== 'function') {
                console.error('QR library is unavailable. Check the internet connection and reload.');
                alert('QR library load nahi hui. Internet connection check karke page reload karein.');
                return;
            }
            // Clear earlier opaque pixels before drawing transparent light modules.
            const context = canvas.getContext('2d');
            context.clearRect(0, 0, canvas.width, canvas.height);
            QRCode.toCanvas(canvas, qrPayload, {
                width: 300,
                margin: 4,
                color: { dark: '#FFFFFFFF', light: '#00000000' }
            }, function (error) {
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
            const canvas = document.getElementById('qrCanvas');
            const size = canvas.getBoundingClientRect().width;
            const containerStyle = getComputedStyle(qrContainer);
            const paddingLeft = (parseFloat(containerStyle.paddingLeft) || 0) + (parseFloat(containerStyle.borderLeftWidth) || 0);
            const paddingTop = (parseFloat(containerStyle.paddingTop) || 0) + (parseFloat(containerStyle.borderTopWidth) || 0);
            const left = qrContainer.offsetLeft + paddingLeft;
            const top = qrContainer.offsetTop + paddingTop;
            interaction = {
                pointerId: event.pointerId,
                mode: handle ? 'resize' : 'drag',
                corner: handle?.dataset.handle,
                startX: point.x,
                startY: point.y,
                left,
                top,
                boxLeft: qrContainer.offsetLeft,
                boxTop: qrContainer.offsetTop,
                boxWidth: qrContainer.offsetWidth,
                boxHeight: qrContainer.offsetHeight,
                paddingLeft,
                paddingTop,
                size
            };
            qrContainer.setPointerCapture(event.pointerId);
        });

        qrContainer.addEventListener('pointermove', event => {
            if (!interaction || event.pointerId !== interaction.pointerId) return;
            const point = cardPoint(event);
            const canvas = document.getElementById('qrCanvas');
            const box = getComputedStyle(qrContainer);
            const paddingRight = parseFloat(box.paddingRight) || 0;
            const paddingBottom = parseFloat(box.paddingBottom) || 0;
            const canvasWidth = canvas.getBoundingClientRect().width;
            const canvasHeight = canvas.getBoundingClientRect().height;
            const totalWidth = canvasWidth + interaction.paddingLeft + paddingRight + 12;
            const totalHeight = canvasHeight + interaction.paddingTop + paddingBottom + 12;
            const maxLeft = Math.max(0, cardParent.clientWidth - totalWidth);
            const maxTop = Math.max(0, cardParent.clientHeight - totalHeight);

            if (interaction.mode === 'drag') {
                const boxLeft = clamp(interaction.boxLeft + point.x - interaction.startX, 0, maxLeft);
                const boxTop = clamp(interaction.boxTop + point.y - interaction.startY, 0, maxTop);
                qrContainer.style.left = `${boxLeft}px`;
                qrContainer.style.top = `${boxTop}px`;
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
            const extraWidth = interaction.paddingLeft + paddingRight + 12;
            const extraHeight = interaction.paddingTop + paddingBottom + 12;
            const maxWidth = xSign < 0 ? fixedX : cardParent.clientWidth - fixedX - extraWidth;
            const maxHeight = ySign < 0 ? fixedY : cardParent.clientHeight - fixedY - extraHeight;
            const maxSize = Math.max(minSize, Math.min(maxWidth, maxHeight));
            const size = clamp(interaction.size + Math.max(dx, dy), minSize, maxSize);
            const left = xSign < 0 ? fixedX - size : fixedX;
            const top = ySign < 0 ? fixedY - size : fixedY;

            canvas.style.width = `${size}px`;
            canvas.style.height = `${size}px`;
            qrContainer.style.width = 'max-content';
            qrContainer.style.height = 'max-content';
            qrContainer.style.left = `${left - interaction.paddingLeft}px`;
            qrContainer.style.top = `${top - interaction.paddingTop}px`;
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

        dropZone.addEventListener('click', event => {
            if (event.target !== imageUpload) imageUpload.click();
        });
        dropZone.addEventListener('keydown', event => {
            if (event.key === 'Enter' || event.key === ' ') {
                event.preventDefault();
                imageUpload.click();
            }
        });

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

        ['dragenter', 'dragover'].forEach(type => dropZone.addEventListener(type, event => {
            event.preventDefault();
            dropZone.classList.add('border-sky-300', 'bg-slate-800');
        }));
        ['dragleave', 'drop'].forEach(type => dropZone.addEventListener(type, event => {
            event.preventDefault();
            dropZone.classList.remove('border-sky-300', 'bg-slate-800');
        }));
        dropZone.addEventListener('drop', event => {
            const file = [...(event.dataTransfer?.files || [])].find(item => item.type.startsWith('image/'));
            if (file) processImage(file);
            else ocrStatus.textContent = 'Image file yahan drop karein.';
        });

        function processImage(file) {
            if (!file || !file.type.startsWith('image/')) {
                ocrStatus.textContent = 'Kripya image file select karein.';
                return;
            }
            if (!window.Tesseract) {
                ocrStatus.textContent = 'OCR library load nahi hui. Internet check karke page reload karein.';
                return;
            }
            ocrStatus.textContent = '🔍 Image read ho rahi hai: 0%';
            Tesseract.recognize(
                file,
                'eng',
                { logger: m => {
                    if (m.status === 'recognizing text') ocrStatus.textContent = `🔍 Image read ho rahi hai: ${Math.round((m.progress || 0) * 100)}%`;
                } }
            ).then(({ data }) => {
                const result = parseExtractedText(data.text, data.words);
                const missing = result.missing.length ? ` Check: ${result.missing.join(', ')}.` : '';
                ocrStatus.textContent = `✅ ${result.filled} fields read; barcode ready.${missing}`;
            }).catch(err => {
                ocrStatus.textContent = '❌ Image read nahi hui. Saaf aur seedhi image try karein.';
                console.error(err);
            });
        }

        function parseExtractedText(text, words = []) {
            const lines = text.split('\n').map(l => l.trim()).filter(l => l.length > 0);
            const fieldPatterns = {
                studentName: /(?:student|candidate)\s*name|^name$/i,
                seatNo: /(?:seat|roll|enrol(?:l)?ment|registration)\s*(?:no\.?|number|#)/i,
                dob: /date\s*of\s*birth|\bdob\b/i,
                yearVal: /\byear\b/i,
                trade: /\btrade\b/i,
                practical: /\bpractical(?:\s*marks?)?\b/i,
                theory: /\btheory(?:\s*marks?)?\b/i,
                wcs: /workshop\s*(?:calculation|calc(?:ulation)?)(?:\s*(?:and|&)\s*science)?|\bwcs\b/i,
                ed: /engineering\s*drawing|\bdrawing\b/i,
                socialStudy: /social\s*study|\bsocial\b/i,
                totalMarks: /total\s*marks|\btotal\b/i,
                cutoff: /out\s*of{0,1}\s*marks|outoff\s*marks|maximum\s*marks/i
            };
            const found = {};
            const knownLabel = new RegExp(Object.values(fieldPatterns).map(p => p.source).join('|'), 'i');
            const nextColumnLabel = /\b(?:student\s*name|candidate\s*name|seat\s*(?:no\.?|number)|roll\s*(?:no\.?|number)|date\s*of\s*birth|birth|dob|year|trade|practical(?:\s*marks?)?|theory(?:\s*marks?)?|workshop(?:\s*(?:calculation|calc))?|calculation|science|engineering|drawing|social(?:\s*study)?|total(?:\s*marks)?|out\s*off\s*marks|out\s*of\s*marks|outoff\s*marks|maximum\s*marks)\b/i;

            // Read labels printed beside values, including labels and values on separate lines.
            lines.forEach((line, index) => {
                const hasSeveralLabels = (line.match(new RegExp(nextColumnLabel.source, 'gi')) || []).length > 1;
                for (const [id, pattern] of Object.entries(fieldPatterns)) {
                    const match = line.match(pattern);
                    if (!match || found[id]) continue;
                    let value = line.slice(match.index + match[0].length).replace(/^\s*[:#\-–|]+\s*/, '').trim();
                    const followingLabel = value.match(nextColumnLabel);
                    if (followingLabel) value = value.slice(0, followingLabel.index).trim();
                    if (!value && !hasSeveralLabels) {
                        const next = lines[index + 1] || '';
                        if (next && !knownLabel.test(next)) value = next;
                    }
                    if (value) found[id] = value;
                }
            });

            // For a table image, use OCR word positions to map cells under their column headings.
            if (Array.isArray(words) && words.length) {
                const columns = [
                    ['studentName', /^(student|candidate)$/i], ['seatNo', /^(seat|roll)$/i],
                    ['dob', /^(birth|dob|date)$/i], ['yearVal', /^year$/i], ['trade', /^trade$/i],
                    ['practical', /^practical$/i], ['theory', /^theory$/i], ['wcs', /^workshop$/i],
                    ['ed', /^engineering$/i], ['socialStudy', /^social$/i], ['totalMarks', /^total$/i],
                    ['cutoff', /^(outoff|outof|max|out)$/i]
                ];
                const anchors = columns.map(([id, pattern]) => {
                    const hit = words.find(word => pattern.test(String(word.text || '').replace(/[^a-z]/gi, '')) && word.bbox);
                    return hit ? { id, x: (hit.bbox.x0 + hit.bbox.x1) / 2, y: hit.bbox.y1 } : null;
                }).filter(Boolean).sort((a, b) => a.x - b.x);
                if (anchors.length >= 5) {
                    const headerWords = /^(student|candidate|name|seat|roll|no|date|of|birth|dob|year|trade|practical|marks|theory|workshop|calculation|science|engineering|drawing|social|study|total|outoff|out|off)$/i;
                    const headerBottom = Math.max(...words.filter(word => word.bbox && headerWords.test(String(word.text || '').replace(/[^a-z]/gi, ''))).map(word => word.bbox.y1), ...anchors.map(anchor => anchor.y)) + 3;
                    const cells = Object.fromEntries(anchors.map(anchor => [anchor.id, []]));
                    words.filter(word => word.bbox && word.bbox.y0 > headerBottom && !headerWords.test(String(word.text || '').replace(/[^a-z]/gi, ''))).forEach(word => {
                        const x = (word.bbox.x0 + word.bbox.x1) / 2;
                        let nearest = 0;
                        anchors.forEach((anchor, i) => { if (Math.abs(anchor.x - x) < Math.abs(anchors[nearest].x - x)) nearest = i; });
                        cells[anchors[nearest].id].push(word);
                    });
                    Object.entries(cells).forEach(([id, cellWords]) => {
                        if (cellWords.length) found[id] = cellWords.sort((a, b) => a.bbox.y0 - b.bbox.y0 || a.bbox.x0 - b.bbox.x0).map(word => word.text).join(' ').trim();
                    });
                }
            }

            // Catch common values even when the image has no explicit labels.
            const allText = lines.join(' ');
            if (!found.seatNo) found.seatNo = allText.match(/\b[A-Z]\d{6,10}\b/i)?.[0];
            if (!found.dob) found.dob = allText.match(/\b\d{4}[-/]\d{2}[-/]\d{2}\b/)?.[0];
            if (!found.yearVal) found.yearVal = allText.match(/\b20\d{2}\s*(?:to|[-–])\s*20\d{2}\b/i)?.[0];

            const ids = Object.keys(fieldPatterns);
            ids.forEach(id => { if (found[id]) document.getElementById(id).value = found[id].replace(/\s+/g, ' ').trim(); });
            if (!found.studentName) {
                const nameGuess = lines.find(line => line.length > 3 && !knownLabel.test(line) && !/\d{4}[-/]\d{2}[-/]\d{2}|\b[A-Z]\d{6,10}\b/i.test(line));
                if (nameGuess) document.getElementById('studentName').value = nameGuess;
            }
            generateCardQR();
            const filled = ids.filter(id => document.getElementById(id).value.trim()).length;
            return { filled, missing: ids.filter(id => !document.getElementById(id).value.trim()).map(id => ({studentName:'Name',seatNo:'Seat No',dob:'DOB',yearVal:'Year',trade:'Trade',practical:'Practical',theory:'Theory',wcs:'Workshop',ed:'Drawing',socialStudy:'Social',totalMarks:'Total',cutoff:'OutOff'}[id])) };
        }

        function showScanResultIfRequested() {
            const raw = new URLSearchParams(location.search).get('result');
            if (!raw) return;
            try {
                const data = JSON.parse(raw);
                const values = [data.name, data.seat, data.dob, data.year, data.trade,
                    data.practical, data.theory, data.wcs, data.ed, data.socialStudy,
                    data.total, data.cutoff];
                const row = document.getElementById('scanResultRow');
                row.replaceChildren(...values.map(value => {
                    const cell = document.createElement('td');
                    cell.textContent = value ?? '';
                    return cell;
                }));
                const officialUrl = new URL(data.officialUrl);
                if (!['https:', 'http:'].includes(officialUrl.protocol)) throw new Error('Invalid official URL');
                document.getElementById('officialResultLink').href = officialUrl.href;
                document.body.classList.add('result-view');
                document.title = 'Student Result - Shiv Nirmal ITI';
            } catch (error) {
                console.error('Could not display scan result:', error);
                document.body.classList.add('result-view');
                document.getElementById('scanResultPage').innerHTML = '<p class="mx-auto max-w-3xl rounded-lg bg-white p-6 text-center text-red-700 shadow">Result link is invalid or incomplete.</p>';
            }
        }

        // Initialize result or QR view on load.
        window.onload = function() {
            showScanResultIfRequested();
            if (!new URLSearchParams(location.search).has('result')) generateCardQR();
        };
    </script>
</body>
</html>
