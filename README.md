<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shiv Nirmal ITI - Smart Auto OCR Result & QR Generator</title>
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
        <div class="max-w-[96%] mx-auto flex flex-col md:flex-row justify-between items-center gap-4">
            <div>
                <h1 class="text-xl font-bold text-amber-400 flex items-center gap-2">
                    ⚡ Shiv Nirmal ITI - Smart Auto OCR Result & QR Generator
                </h1>
                <p class="text-xs text-slate-400">Paste/Upload image to auto-fill empty fields, generate card & embedded QR</p>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="max-w-[96%] mx-auto p-4 md:p-6 grid grid-cols-1 lg:grid-cols-12 gap-6">
        
        <!-- Left Panel: Input Fields -->
        <section class="lg:col-span-5 bg-slate-800 border border-slate-700 rounded-xl p-5 shadow-lg flex flex-col gap-3">
            <h2 class="text-lg font-semibold text-sky-400 border-b border-slate-700 pb-2">📥 Smart OCR Auto-Fill & Manual Input Box</h2>
            
            <!-- Paste or Upload Box -->
            <div class="bg-slate-900 border-2 border-dashed border-sky-500/50 rounded-lg p-3 text-center cursor-pointer hover:border-sky-400 transition focus:outline-none" id="dropZone" tabindex="0">
                <p class="text-xs font-bold text-sky-300">📋 Click here & Press Ctrl+V to Paste Result Image</p>
                <p class="text-[10px] text-slate-400 mt-1">Or choose an image file:</p>
                <input type="file" id="imageUpload" accept="image/*" class="mt-1 text-xs text-slate-300 file:mr-2 file:py-1 file:px-3 file:rounded file:border-0 file:text-xs file:font-semibold file:bg-sky-600 file:text-white hover:file:bg-sky-500">
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
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Workshop Calc & Science:</label>
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
                    <input type="text" id="totalMarks" placeholder="Auto-calculated or manual" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none font-bold text-amber-400">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">OutOff Marks:</label>
                    <input type="text" id="cutoff" value="700" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200 outline-none">
                </div>
            </div>

            <button onclick="generateCardQR()" class="mt-2 w-full bg-blue-600 hover:bg-blue-500 text-white font-bold py-2.5 rounded-lg shadow text-xs">
                🚀 Generate Card & QR
            </button>
        </section>

        <!-- Right Panel: Preview Layout -->
        <section class="lg:col-span-7 flex flex-col gap-6">
            <div class="bg-slate-800 border border-slate-700 rounded-xl p-5 shadow-lg overflow-x-auto">
                <div class="flex justify-between items-center border-b border-slate-700 pb-2 mb-4">
                    <h2 class="text-lg font-semibold text-emerald-400">📄 Result Card Layout Preview</h2>
                    <button onclick="downloadCardImage()" class="bg-emerald-600 hover:bg-emerald-500 text-white text-xs font-bold px-3 py-1.5 rounded transition">
                        📥 Download Card Image
                    </button>
                </div>
                
                <!-- Bordered Box Card Container -->
                <div id="captureCard" class="bg-white text-slate-800 p-4 rounded-lg border-2 border-slate-400 shadow-md flex flex-col gap-4 min-w-[700px]">
                    <div class="flex justify-between items-center border-b-2 border-slate-300 pb-2">
                        <div>
                            <h3 class="font-bold text-base text-slate-900 uppercase">Shiv Nirmal ITI</h3>
                            <p class="text-xs text-slate-500">Official Portal Result Verification Card</p>
                        </div>
                        <div class="bg-white p-1 border border-slate-300 rounded">
                            <canvas id="qrCanvas" class="w-24 h-24"></canvas>
                        </div>
                    </div>

                    <!-- Result Table -->
                    <div class="overflow-x-auto">
                        <table class="w-full border-collapse border border-slate-400 text-[10px] text-center">
                            <thead>
                                <tr class="bg-slate-100 text-slate-700">
                                    <th class="border border-slate-400 p-1.5">Student Name</th>
                                    <th class="border border-slate-400 p-1.5">Seat No</th>
                                    <th class="border border-slate-400 p-1.5">Date Of Birth</th>
                                    <th class="border border-slate-400 p-1.5">Year</th>
                                    <th class="border border-slate-400 p-1.5">Trade</th>
                                    <th class="border border-slate-400 p-1.5">Practical Marks</th>
                                    <th class="border border-slate-400 p-1.5">Theory Marks</th>
                                    <th class="border border-slate-400 p-1.5">Workshop Calculation Science</th>
                                    <th class="border border-slate-400 p-1.5">Engineering Drawing</th>
                                    <th class="border border-slate-400 p-1.5">Social Study</th>
                                    <th class="border border-slate-400 p-1.5">Total Marks</th>
                                    <th class="border border-slate-400 p-1.5">OutOff Marks</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td id="lblStudentName" class="border border-slate-400 p-1.5 font-medium">-</td>
                                    <td id="lblSeatNo" class="border border-slate-400 p-1.5 font-bold text-blue-600">-</td>
                                    <td id="lblDob" class="border border-slate-400 p-1.5">-</td>
                                    <td id="lblYear" class="border border-slate-400 p-1.5">-</td>
                                    <td id="lblTrade" class="border border-slate-400 p-1.5">-</td>
                                    <td id="lblPractical" class="border border-slate-400 p-1.5">-</td>
                                    <td id="lblTheory" class="border border-slate-400 p-1.5">-</td>
                                    <td id="lblWcs" class="border border-slate-400 p-1.5">-</td>
                                    <td id="lblEd" class="border border-slate-400 p-1.5">-</td>
                                    <td id="lblSocialStudy" class="border border-slate-400 p-1.5">-</td>
                                    <td id="lblTotal" class="border border-slate-400 p-1.5 font-bold text-emerald-700">-</td>
                                    <td id="lblCutoff" class="border border-slate-400 p-1.5">700</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>

                    <!-- Portal Link Box -->
                    <div class="border-t-2 border-slate-300 pt-2 flex justify-between items-center text-[10px]">
                        <span class="text-slate-600 font-semibold">🔗 Official Search Portal Link:</span>
                        <a id="lblPortalLink" href="#" target="_blank" class="text-blue-600 underline font-bold truncate max-w-[400px]">#</a>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <script>
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

            document.getElementById('lblStudentName').innerText = studentName;
            document.getElementById('lblSeatNo').innerText = seatNo;
            document.getElementById('lblDob').innerText = dob;
            document.getElementById('lblYear').innerText = yearVal;
            document.getElementById('lblTrade').innerText = trade;
            document.getElementById('lblPractical').innerText = practical;
            document.getElementById('lblTheory').innerText = theory;
            document.getElementById('lblWcs').innerText = wcs;
            document.getElementById('lblEd').innerText = ed;
            document.getElementById('lblSocialStudy').innerText = socialStudy;
            document.getElementById('lblTotal').innerText = totalMarks;
            document.getElementById('lblCutoff').innerText = cutoff;

            const targetUrl = `${baseUrl}?course=${encodeURIComponent(courseVal)}&seat=${encodeURIComponent(seatNo)}`;
            const linkElement = document.getElementById('lblPortalLink');
            linkElement.href = targetUrl;
            linkElement.innerText = targetUrl;

            const qrPayload = `=========================\nSHIV NIRMAL ITI\n=========================\nStudent Name: ${studentName}\nSeat No: ${seatNo}\nDOB: ${dob}\nYear: ${yearVal}\nTrade: ${trade}\nPractical: ${practical}\nTheory: ${theory}\nWorkshop Calc & Sci: ${wcs}\nEngineering Drawing: ${ed}\nSocial Study: ${socialStudy}\nTotal: ${totalMarks} / ${cutoff}\n-------------------------\nSearch Link:\n${targetUrl}`;

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
                    saveAs(blob, `Result_Card_${document.getElementById('seatNo').value || 'Data'}.png`);
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
            console.log("Extracted OCR Text:\n", text);
            const lines = text.split('\n').map(l => l.trim()).filter(l => l.length > 0);

            // Clear inputs
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
    </script>
</body>
</html>
