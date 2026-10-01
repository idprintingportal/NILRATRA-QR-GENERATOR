<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shiv Nirmal ITI - Smart Result & QR Generator</title>
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
</head>
<body class="bg-slate-900 text-slate-100 min-h-screen">

    <!-- Header -->
    <header class="bg-slate-800 border-b border-slate-700 py-4 px-6 shadow-md">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-center gap-4">
            <div>
                <h1 class="text-xl font-bold text-amber-400 flex items-center gap-2">
                    ⚡ Shiv Nirmal ITI - Smart Result & QR Generator
                </h1>
                <p class="text-xs text-slate-400">Auto-fill via image paste/upload, bordered card preview & QR embedding</p>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="max-w-7xl mx-auto p-4 md:p-6 grid grid-cols-1 lg:grid-cols-12 gap-6">
        
        <!-- Left Panel: Smart Paste/Upload & Manual Data Inputs -->
        <section class="lg:col-span-5 bg-slate-800 border border-slate-700 rounded-xl p-5 shadow-lg flex flex-col gap-3">
            <h2 class="text-lg font-semibold text-sky-400 border-b border-slate-700 pb-2">📥 Smart OCR & Data Inputs</h2>
            
            <!-- Paste or Upload Box -->
            <div class="bg-slate-900 border-2 border-dashed border-sky-500/50 rounded-lg p-4 text-center cursor-pointer hover:border-sky-400 transition" id="dropZone" contenteditable="true">
                <p class="text-xs font-bold text-sky-300">📋 Click here & Press Ctrl+V to Paste Result Image</p>
                <p class="text-[10px] text-slate-400 mt-1">Or upload image file:</p>
                <input type="file" id="imageUpload" accept="image/*" class="mt-2 text-xs text-slate-300 file:mr-2 file:py-1 file:px-3 file:rounded file:border-0 file:text-xs file:font-semibold file:bg-sky-600 file:text-white hover:file:bg-sky-500">
                <p id="ocrStatus" class="text-[10px] text-amber-400 mt-2 font-medium"></p>
            </div>

            <div class="grid grid-cols-2 gap-2 mt-1">
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
                    <input type="text" id="studentName" value="Roshan Bistur sawara" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Seat Number:</label>
                    <input type="text" id="seatNo" value="A1321789" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
            </div>

            <div class="grid grid-cols-2 gap-2">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Date Of Birth:</label>
                    <input type="text" id="dob" value="2002-06-09" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Year:</label>
                    <input type="text" id="yearVal" value="2023 to 2025" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
            </div>

            <div class="grid grid-cols-2 gap-2">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Trade:</label>
                    <input type="text" id="trade" value="Electrician" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Practical Marks:</label>
                    <input type="text" id="practical" value="331,336" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
            </div>

            <div class="grid grid-cols-3 gap-2">
                <div>
                    <label class="block text-[10px] font-bold text-slate-300 uppercase mb-1">Theory Marks:</label>
                    <input type="text" id="theory" value="89,92" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
                <div>
                    <label class="block text-[10px] font-bold text-slate-300 uppercase mb-1">Total Marks:</label>
                    <input type="text" id="totalMarks" value="557,563" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
                <div>
                    <label class="block text-[10px] font-bold text-slate-300 uppercase mb-1">OutOff Marks:</label>
                    <input type="text" id="cutoff" value="700" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
            </div>

            <button onclick="generateCardQR()" class="mt-2 w-full bg-blue-600 hover:bg-blue-500 text-white font-bold py-2.5 rounded-lg shadow text-xs">
                🚀 Update Card & Generate QR
            </button>
        </section>

        <!-- Right Panel: Preview Layout with Boxes & Lines -->
        <section class="lg:col-span-7 flex flex-col gap-6">
            
            <div class="bg-slate-800 border border-slate-700 rounded-xl p-5 shadow-lg">
                <div class="flex justify-between items-center border-b border-slate-700 pb-2 mb-4">
                    <h2 class="text-lg font-semibold text-emerald-400">📄 Result Card Layout Preview</h2>
                    <button onclick="downloadCardImage()" class="bg-emerald-600 hover:bg-emerald-500 text-white text-xs font-bold px-3 py-1.5 rounded transition">
                        📥 Download Card Image
                    </button>
                </div>
                
                <!-- Bordered Box Card Container matching portal style -->
                <div id="captureCard" class="bg-white text-slate-800 p-4 rounded-lg border-2 border-slate-400 shadow-md flex flex-col gap-4">
                    <div class="flex justify-between items-center border-b-2 border-slate-300 pb-2">
                        <div>
                            <h3 class="font-bold text-sm text-slate-900 uppercase">Shiv Nirmal ITI</h3>
                            <p class="text-[10px] text-slate-500">Official Portal Result Verification Card</p>
                        </div>
                        <div class="bg-white p-1 border border-slate-300 rounded">
                            <canvas id="qrCanvas" class="w-24 h-24"></canvas>
                        </div>
                    </div>

                    <!-- Table with explicit borders and boxes -->
                    <div class="overflow-x-auto">
                        <table class="w-full border-collapse border border-slate-400 text-[11px] text-center">
                            <thead>
                                <tr class="bg-slate-100 text-slate-700">
                                    <th class="border border-slate-400 p-1.5">Student Name</th>
                                    <th class="border border-slate-400 p-1.5">Seat No</th>
                                    <th class="border border-slate-400 p-1.5">Date Of Birth</th>
                                    <th class="border border-slate-400 p-1.5">Year</th>
                                    <th class="border border-slate-400 p-1.5">Trade</th>
                                    <th class="border border-slate-400 p-1.5">Practical</th>
                                    <th class="border border-slate-400 p-1.5">Theory</th>
                                    <th class="border border-slate-400 p-1.5">Total</th>
                                    <th class="border border-slate-400 p-1.5">OutOff</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td id="lblStudentName" class="border border-slate-400 p-1.5 font-medium">Roshan Bistur sawara</td>
                                    <td id="lblSeatNo" class="border border-slate-400 p-1.5 font-bold text-blue-600">A1321789</td>
                                    <td id="lblDob" class="border border-slate-400 p-1.5">2002-06-09</td>
                                    <td id="lblYear" class="border border-slate-400 p-1.5">2023 to 2025</td>
                                    <td id="lblTrade" class="border border-slate-400 p-1.5">Electrician</td>
                                    <td id="lblPractical" class="border border-slate-400 p-1.5">331,336</td>
                                    <td id="lblTheory" class="border border-slate-400 p-1.5">89,92</td>
                                    <td id="lblTotal" class="border border-slate-400 p-1.5 font-bold">557,563</td>
                                    <td id="lblCutoff" class="border border-slate-400 p-1.5">700</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>

                    <!-- Original Portal Link Box at the bottom -->
                    <div class="border-t-2 border-slate-300 pt-2 flex justify-between items-center text-[10px]">
                        <span class="text-slate-600 font-semibold">🔗 Official Search Portal Link:</span>
                        <a id="lblPortalLink" href="https://nemrc.co.in/result.php" target="_blank" class="text-blue-600 underline font-bold truncate max-w-[280px]">https://nemrc.co.in/result.php?course=ITI&seat=A1321789</a>
                    </div>
                </div>
            </div>

        </section>
    </main>

    <script>
        function generateCardQR() {
            const baseUrl = document.getElementById('baseUrl').value.trim();
            const courseVal = document.getElementById('courseVal').value.trim();
            const seatNo = document.getElementById('seatNo').value.trim();
            const studentName = document.getElementById('studentName').value.trim();
            const dob = document.getElementById('dob').value.trim();
            const yearVal = document.getElementById('yearVal').value.trim();
            const trade = document.getElementById('trade').value.trim();
            const practical = document.getElementById('practical').value.trim();
            const theory = document.getElementById('theory').value.trim();
            const totalMarks = document.getElementById('totalMarks').value.trim();
            const cutoff = document.getElementById('cutoff').value.trim();

            document.getElementById('lblStudentName').innerText = studentName;
            document.getElementById('lblSeatNo').innerText = seatNo;
            document.getElementById('lblDob').innerText = dob;
            document.getElementById('lblYear').innerText = yearVal;
            document.getElementById('lblTrade').innerText = trade;
            document.getElementById('lblPractical').innerText = practical;
            document.getElementById('lblTheory').innerText = theory;
            document.getElementById('lblTotal').innerText = totalMarks;
            document.getElementById('lblCutoff').innerText = cutoff;

            const targetUrl = `${baseUrl}?course=${encodeURIComponent(courseVal)}&seat=${encodeURIComponent(seatNo)}`;
            const linkElement = document.getElementById('lblPortalLink');
            linkElement.href = targetUrl;
            linkElement.innerText = targetUrl;

            const qrPayload = `=========================\nSHIV NIRMAL ITI\n=========================\nStudent Name: ${studentName}\nSeat No: ${seatNo}\nDOB: ${dob}\nYear: ${yearVal}\nTrade: ${trade}\nPractical: ${practical}\nTheory: ${theory}\nTotal: ${totalMarks} / ${cutoff}\n-------------------------\nSearch Link:\n${targetUrl}`;

            const canvas = document.getElementById('qrCanvas');
            setTimeout(() => {
                QRCode.toCanvas(canvas, qrPayload, { width: 140, margin: 1 }, function (error) {
                    if (error) console.error("QR Generation Error:", error);
                });
            }, 50);
        }

        function downloadCardImage() {
            const cardElement = document.getElementById('captureCard');
            html2canvas(cardElement, { scale: 2 }).then(canvas => {
                canvas.toBlob(function(blob) {
                    saveAs(blob, `Result_Card_${document.getElementById('seatNo').value}.png`);
                });
            });
        }

        // Image Paste & OCR Processing Handler
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
            ocrStatus.innerText = "🔍 Scanning image and extracting text...";
            Tesseract.recognize(
                file,
                'eng',
                { logger: m => console.log(m) }
            ).then(({ data: { text } }) => {
                ocrStatus.innerText = "✅ Data extracted successfully!";
                parseExtractedText(text);
            }).catch(err => {
                ocrStatus.innerText = "❌ Error reading image. Try another image.";
                console.error(err);
            });
        }

        function parseExtractedText(text) {
            console.log("OCR Text:", text);
            // Simple regex match patterns for seat number (e.g. A followed by numbers or alphanumeric code)
            const seatMatch = text.match(/[A-Z0-9]{7,10}/);
            if (seatMatch) {
                document.getElementById('seatNo').value = seatMatch[0];
            }
            // You can auto-fill other fields based on patterns or keep manual adjustment
            generateCardQR();
        }

        window.onload = function() {
            generateCardQR();
        };
    </script>
</body>
</html>
