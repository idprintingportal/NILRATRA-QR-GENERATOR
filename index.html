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
        }
        #qrResizeHandle {
            position: absolute;
            right: -6px;
            bottom: -6px;
            width: 14px;
            height: 14px;
            background-color: #0284c7;
            border: 2px solid #ffffff;
            border-radius: 50%;
            cursor: nwse-resize;
            z-index: 40;
        }
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
                        <!-- Resize Handle -->
                        <div id="qrResizeHandle" title="Drag corner to resize Barcode"></div>
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

            const targetUrl = `${baseUrl}?course=${encodeURIComponent(courseVal)}&seat=${encodeURIComponent(seatNo)}`;

            // QR code payload
            const qrPayload = `=========================\nSHIV NIRMAL ITI\n=========================\nStudent Name: ${studentName}\nSeat No: ${seatNo}\nDOB: ${dob}\nYear: ${yearVal}\nTrade: ${trade}\nPractical: ${practical}\nTheory: ${theory}\nWorkshop Calc & Sci: ${wcs}\nEngineering Drawing: ${ed}\nSocial Study: ${socialStudy}\nTotal: ${totalMarks} / ${cutoff}\n-------------------------\nOfficial Result Search Link:\n${targetUrl}`;

            const canvas = document.getElementById('qrCanvas');
            setTimeout(() => {
                QRCode.toCanvas(canvas, qrPayload, { width: 300, margin: 1 }, function (error) {
                    if (error) console.error("QR Generation Error:", error);
                });
            }, 50);
        }

        // Export/Download Image with Barcode Overlay
        function downloadCardImage() {
            const cardElement = document.getElementById('captureCard');
            const qrContainer = document.getElementById('qrMovableContainer');
            const resizeHandle = document.getElementById('qrResizeHandle');

            // Hide dashed border and handles for clean download output
            qrContainer.classList.remove('border-2', 'border-dashed', 'border-sky-500');
            resizeHandle.style.display = 'none';

            html2canvas(cardElement, { scale: 3, useCORS: true, backgroundColor: null }).then(canvas => {
                // Restore borders & handle
                qrContainer.classList.add('border-2', 'border-dashed', 'border-sky-500');
                resizeHandle.style.display = 'block';

                canvas.toBlob(function(blob) {
                    saveAs(blob, `Result_Barcode_Image_${document.getElementById('seatNo').value || 'Data'}.png`);
                });
            });
        }

        // --- MOVABLE AND RESIZABLE BARCODE LOGIC ---
        const qrContainer = document.getElementById('qrMovableContainer');
        const resizeHandle = document.getElementById('qrResizeHandle');
        const cardParent = document.getElementById('captureCard');

        let isDragging = false;
        let isResizing = false;
        let startX, startY, startWidth, startHeight, startLeft, startTop;

        // Drag & Move Logic
        qrContainer.addEventListener('mousedown', function(e) {
            if (e.target === resizeHandle) return;
            isDragging = true;
            startX = e.clientX;
            startY = e.clientY;
            
            const rect = qrContainer.getBoundingClientRect();
            const parentRect = cardParent.getBoundingClientRect();
            
            startLeft = rect.left - parentRect.left;
            startTop = rect.top - parentRect.top;

            document.addEventListener('mousemove', onMouseMoveDrag);
            document.addEventListener('mouseup', onMouseUp);
        });

        function onMouseMoveDrag(e) {
            if (!isDragging) return;
            const dx = e.clientX - startX;
            const dy = e.clientY - startY;

            let newLeft = startLeft + dx;
            let newTop = startTop + dy;

            const parentRect = cardParent.getBoundingClientRect();
            const containerRect = qrContainer.getBoundingClientRect();

            if (newLeft < 0) newLeft = 0;
            if (newTop < 0) newTop = 0;
            if (newLeft + containerRect.width > parentRect.width) newLeft = parentRect.width - containerRect.width;
            if (newTop + containerRect.height > parentRect.height) newTop = parentRect.height - containerRect.height;

            qrContainer.style.left = newLeft + 'px';
            qrContainer.style.top = newTop + 'px';
            qrContainer.style.right = 'auto';
        }

        // Resize Logic
        resizeHandle.addEventListener('mousedown', function(e) {
            e.stopPropagation();
            isResizing = true;
            startX = e.clientX;
            startY = e.clientY;
            startWidth = qrContainer.offsetWidth;
            startHeight = qrContainer.offsetHeight;

            document.addEventListener('mousemove', onMouseMoveResize);
            document.addEventListener('mouseup', onMouseUp);
        });

        function onMouseMoveResize(e) {
            if (!isResizing) return;
            const dx = e.clientX - startX;
            const dy = e.clientY - startY;

            let newSize = Math.max(50, Math.max(startWidth + dx, startHeight + dy));

            qrContainer.style.width = newSize + 'px';
            qrContainer.style.height = newSize + 'px';
        }

        function onMouseUp() {
            isDragging = false;
            isResizing = false;
            document.removeEventListener('mousemove', onMouseMoveDrag);
            document.removeEventListener('mousemove', onMouseMoveResize);
            document.removeEventListener('mouseup', onMouseUp);
        }

        // OCR Processing Handler
        const dropZone = document.getElementById('dropZone');
        const imageUpload = document.getElementById('imageUpload');
        const ocrStatus = document.getElementById('ocrStatus');

        dropZone.addEventListener('paste', function(e) {
            const items = (e.clipboardData || e.originalEvent.clipboardData).items;
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
