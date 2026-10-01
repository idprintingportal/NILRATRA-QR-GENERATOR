<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OnePlus Maha E-Seva Kendra - Portal QR & Result Card Generator</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- QR Code Library -->
    <script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.1/build/qrcode.min.js"></script>
    <!-- html2canvas for card image export -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <!-- JSZip Library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
    <!-- FileSaver Library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/FileSaver.js/2.0.5/FileSaver.min.js"></script>
</head>
<body class="bg-slate-900 text-slate-100 min-h-screen">

    <!-- Header -->
    <header class="bg-slate-800 border-b border-slate-700 py-4 px-6 shadow-md">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-center gap-4">
            <div>
                <h1 class="text-xl font-bold text-amber-400 flex items-center gap-2">
                    ⚡ OnePlus Maha E-Seva Kendra - Result Layout & QR Generator
                </h1>
                <p class="text-xs text-slate-400">Generate bordered result cards with auto-search QR codes</p>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="max-w-7xl mx-auto p-4 md:p-6 grid grid-cols-1 lg:grid-cols-12 gap-6">
        
        <!-- Left Panel: Manual Data Inputs -->
        <section class="lg:col-span-5 bg-slate-800 border border-slate-700 rounded-xl p-5 shadow-lg flex flex-col gap-3">
            <h2 class="text-lg font-semibold text-sky-400 border-b border-slate-700 pb-2">⚙️ Portal & Student Details</h2>
            
            <div class="grid grid-cols-2 gap-2">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Base URL:</label>
                    <input type="text" id="baseUrl" value="https://nemrc.co.in/result.php" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Course:</label>
                    <input type="text" id="courseVal" value="ITI" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200">
                </div>
            </div>

            <div class="grid grid-cols-2 gap-2">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Student Name:</label>
                    <input type="text" id="studentName" value="Roshan Bistur sawara" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Seat Number:</label>
                    <input type="text" id="seatNo" value="A1321789" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200">
                </div>
            </div>

            <div class="grid grid-cols-2 gap-2">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Date Of Birth:</label>
                    <input type="text" id="dob" value="2002-06-09" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Year:</label>
                    <input type="text" id="yearVal" value="2023 to 2025" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200">
                </div>
            </div>

            <div class="grid grid-cols-2 gap-2">
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Trade:</label>
                    <input type="text" id="trade" value="Electrician" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200">
                </div>
                <div>
                    <label class="block text-[11px] font-bold text-slate-300 uppercase mb-1">Practical Marks:</label>
                    <input type="text" id="practical" value="331,336" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200">
                </div>
            </div>

            <div class="grid grid-cols-3 gap-2">
                <div>
                    <label class="block text-[10px] font-bold text-slate-300 uppercase mb-1">Theory Marks:</label>
                    <input type="text" id="theory" value="89,92" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200">
                </div>
                <div>
                    <label class="block text-[10px] font-bold text-slate-300 uppercase mb-1">Total Marks:</label>
                    <input type="text" id="totalMarks" value="557,563" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200">
                </div>
                <div>
                    <label class="block text-[10px] font-bold text-slate-300 uppercase mb-1">OutOff Marks:</label>
                    <input type="text" id="cutoff" value="700" class="w-full bg-slate-900 border border-slate-700 rounded p-2 text-xs text-slate-200">
                </div>
            </div>

            <button onclick="generateCardQR()" class="mt-2 w-full bg-blue-600 hover:bg-blue-500 text-white font-bold py-2.5 rounded-lg shadow transition duration-200 text-xs">
                🚀 Generate Bordered Result Card & QR
            </button>
        </section>

        <!-- Right Panel: Preview Layout with Boxes & Lines -->
        <section class="lg:col-span-7 flex flex-col gap-6">
            
            <div class="bg-slate-800 border border-slate-700 rounded-xl p-5 shadow-lg">
                <div class="flex justify-between items-center border-b border-slate-700 pb-2 mb-4">
                    <h2 class="text-lg font-semibold text-emerald-400">📄 Result Card Layout Preview</h2>
                    <div class="flex gap-2">
                        <button onclick="downloadCardImage()" class="bg-emerald-600 hover:bg-emerald-500 text-white text-xs font-bold px-3 py-1.5 rounded transition">
                            📥 Download Card
                        </button>
                    </div>
                </div>
                
                <!-- Bordered Box Card Container matching portal style -->
                <div id="captureCard" class="bg-white text-slate-800 p-4 rounded-lg border-2 border-slate-400 shadow-md flex flex-col gap-4">
                    <div class="flex justify-between items-center border-b-2 border-slate-300 pb-2">
                        <div>
                            <h3 class="font-bold text-sm text-slate-900 uppercase">OnePlus Maha E-Seva Kendra</h3>
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
                    <div class="text-[9px] text-slate-400 text-right">Scan QR code to auto-copy seat number & open search portal.</div>
                </div>
            </div>

            <!-- Tampermonkey Script Helper Box -->
            <div class="bg-slate-800 border border-slate-700 rounded-xl p-5 shadow-lg">
                <h2 class="text-lg font-semibold text-amber-400 border-b border-slate-700 pb-2 mb-2">📜 Tampermonkey Auto-Copy Script</h2>
                <textarea readonly rows="5" class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2 font-mono text-[11px] text-sky-300 focus:outline-none">// ==UserScript==
// @name         Auto Copy Seat Number & Course
// @namespace    http://tampermonkey.net/
// @version      1.1
// @match        https://nemrc.co.in/*
// @grant        navigator.clipboard
// ==/UserScript==

(function() {
    'use strict';
    window.addEventListener('load', function() {
        const urlParams = new URLSearchParams(window.location.search);
        const seatNo = urlParams.get('seat');
        const course = urlParams.get('course');
        if (seatNo) {
            if (course) {
                const selectBox = document.querySelector('select');
                if (selectBox) { selectBox.value = course; selectBox.dispatchEvent(new Event('change', { bubbles: true })); }
            }
            setTimeout(() => {
                if (navigator.clipboard && navigator.clipboard.writeText) { navigator.clipboard.writeText(seatNo); }
                const notification = document.createElement('div');
                notification.innerHTML = `📋 Seat Number <b>${seatNo}</b> Copied! Just Paste (Ctrl+V) in search box.`;
                notification.style.cssText = 'position:fixed;top:20px;right:20px;background:#10b981;color:#fff;padding:12px 20px;border-radius:8px;z-index:99999;font-family:sans-serif;font-size:14px;box-shadow:0 4px 12px rgba(0,0,0,0.3);';
                document.body.appendChild(notification);
                setTimeout(() => notification.remove(), 4000);
            }, 600);
        }
    });
})();</textarea>
            </div>

        </section>
    </main>

    <script>
        function generateCardQR() {
            const baseUrl = document.getElementById('baseUrl').value.trim();
            const courseVal = document.getElementById('courseVal').value.trim();
            const seatNo = document.getElementById('seatNo').value.trim();
            
            // Update table preview texts
            document.getElementById('lblStudentName').innerText = document.getElementById('studentName').value;
            document.getElementById('lblSeatNo').innerText = seatNo;
            document.getElementById('lblDob').innerText = document.getElementById('dob').value;
            document.getElementById('lblYear').innerText = document.getElementById('yearVal').value;
            document.getElementById('lblTrade').innerText = document.getElementById('trade').value;
            document.getElementById('lblPractical').innerText = document.getElementById('practical').value;
            document.getElementById('lblTheory').innerText = document.getElementById('theory').value;
            document.getElementById('lblTotal').innerText = document.getElementById('totalMarks').value;
            document.getElementById('lblCutoff').innerText = document.getElementById('cutoff').value;

            const targetUrl = `${baseUrl}?course=${encodeURIComponent(courseVal)}&seat=${encodeURIComponent(seatNo)}`;

            const canvas = document.getElementById('qrCanvas');
            QRCode.toCanvas(canvas, targetUrl, { width: 120, margin: 1 }, function (error) {
                if (error) console.error("QR Error:", error);
            });
        }

        function downloadCardImage() {
            const cardElement = document.getElementById('captureCard');
            html2canvas(cardElement, { scale: 2 }).then(canvas => {
                canvas.toBlob(function(blob) {
                    saveAs(blob, `Result_Card_${document.getElementById('seatNo').value}.png`);
                });
            });
        }

        // Auto generate on load
        window.onload = function() {
            generateCardQR();
        };
    </script>
</body>
</html>
