<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OnePlus Maha E-Seva Kendra - Portal QR & Auto-Copy Tool</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- QR Code Library -->
    <script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.1/build/qrcode.min.js"></script>
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
                    ⚡ OnePlus Maha E-Seva Kendra - QR Portal Automation
                </h1>
                <p class="text-xs text-slate-400">Generate QR codes with download, image copy & auto-copy seat number features</p>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="max-w-7xl mx-auto p-4 md:p-6 grid grid-cols-1 lg:grid-cols-12 gap-6">
        
        <!-- Left Panel: Configuration -->
        <section class="lg:col-span-5 bg-slate-800 border border-slate-700 rounded-xl p-5 shadow-lg flex flex-col gap-4">
            <h2 class="text-lg font-semibold text-sky-400 border-b border-slate-700 pb-2">⚙️ Portal Configuration</h2>
            
            <div>
                <label class="block text-xs font-bold text-slate-300 uppercase mb-1">Portal Result Link (Base URL):</label>
                <input type="text" id="baseUrl" value="https://nemrc.co.in/result.php" class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-slate-200 focus:outline-none focus:border-sky-500">
            </div>

            <div>
                <label class="block text-xs font-bold text-slate-300 uppercase mb-1">Course / Dropdown Value:</label>
                <input type="text" id="courseVal" value="ITI" class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-slate-200 focus:outline-none focus:border-sky-500">
            </div>

            <div>
                <label class="block text-xs font-bold text-slate-300 uppercase mb-1">Seat Numbers (Comma Separated):</label>
                <textarea id="seatsInput" rows="4" class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-slate-200 focus:outline-none focus:border-sky-500" placeholder="A1321789, A1321790">A1321789, A1321790</textarea>
                <p class="text-[10px] text-slate-400 mt-1">Har ek seat number ke liye alag QR code banega.</p>
            </div>

            <button onclick="generateQRs()" class="w-full bg-blue-600 hover:bg-blue-500 text-white font-bold py-3 rounded-lg shadow transition duration-200 text-sm">
                🚀 Generate QRs & ZIP Package
            </button>
        </section>

        <!-- Right Panel: Output & Script -->
        <section class="lg:col-span-7 flex flex-col gap-6">
            
            <!-- Generated Results Box -->
            <div class="bg-slate-800 border border-slate-700 rounded-xl p-5 shadow-lg">
                <div class="flex justify-between items-center border-b border-slate-700 pb-2 mb-4">
                    <h2 class="text-lg font-semibold text-emerald-400">📦 Generated QRs</h2>
                    <button id="downloadZipBtn" onclick="downloadAllZip()" class="hidden bg-emerald-600 hover:bg-emerald-500 text-white text-xs font-bold px-3 py-1.5 rounded transition">
                        📥 Download All (ZIP)
                    </button>
                </div>
                
                <div id="qrContainer" class="grid grid-cols-1 sm:grid-cols-2 gap-4 max-h-[400px] overflow-y-auto pr-2">
                    <p class="text-slate-400 text-sm italic col-span-2 text-center py-8">Configure details on left and click Generate.</p>
                </div>
            </div>

            <!-- Tampermonkey Script Helper Box -->
            <div class="bg-slate-800 border border-slate-700 rounded-xl p-5 shadow-lg">
                <h2 class="text-lg font-semibold text-amber-400 border-b border-slate-700 pb-2 mb-2">📜 Tampermonkey Auto-Copy Script</h2>
                <p class="text-xs text-slate-300 mb-2">Is script ko apne Tampermonkey extension mein dalein taaki link khulte hi seat number automatic copy ho jaye:</p>
                <textarea readonly rows="6" class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2 font-mono text-[11px] text-sky-300 focus:outline-none">// ==UserScript==
// @name         Auto Copy Seat Number & Course
// @namespace    http://tampermonkey.net/
// @version      1.1
// @match        https://nemrc.co.in/*
// @grant        GM_setClipboard
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
                if (selectBox) {
                    selectBox.value = course;
                    selectBox.dispatchEvent(new Event('change', { bubbles: true }));
                }
            }

            setTimeout(() => {
                if (navigator.clipboard && navigator.clipboard.writeText) {
                    navigator.clipboard.writeText(seatNo);
                } else {
                    const textArea = document.createElement("textarea");
                    textArea.value = seatNo;
                    document.body.appendChild(textArea);
                    textArea.select();
                    document.execCommand("copy");
                    document.body.removeChild(textArea);
                }

                const notification = document.createElement('div');
                notification.innerHTML = `📋 Seat Number <b>${seatNo}</b> Copied! Just Paste (Ctrl+V) in search box.`;
                notification.style.position = 'fixed';
                notification.style.top = '20px';
                notification.style.right = '20px';
                notification.style.background = '#10b981';
                notification.style.color = '#fff';
                notification.style.padding = '12px 20px';
                notification.style.borderRadius = '8px';
                notification.style.zIndex = '99999';
                notification.style.fontFamily = 'sans-serif';
                notification.style.fontSize = '14px';
                document.body.appendChild(notification);

                setTimeout(() => {
                    notification.remove();
                }, 4000);

            }, 600);
        }
    });
})();</textarea>
            </div>

        </section>
    </main>

    <script>
        let generatedData = [];

        function generateQRs() {
            const baseUrl = document.getElementById('baseUrl').value.trim();
            const courseVal = document.getElementById('courseVal').value.trim();
            const seatsRaw = document.getElementById('seatsInput').value;
            const seats = seatsRaw.split(',').map(s => s.trim()).filter(s => s.length > 0);
            
            const container = document.getElementById('qrContainer');
            container.innerHTML = '';
            generatedData = [];

            if (!baseUrl || seats.length === 0) {
                container.innerHTML = '<p class="text-red-400 text-sm col-span-2 text-center">Please enter a valid base URL and seat numbers.</p>';
                document.getElementById('downloadZipBtn').classList.add('hidden');
                return;
            }

            seats.forEach((seat, index) => {
                const targetUrl = `${baseUrl}?course=${encodeURIComponent(courseVal)}&seat=${encodeURIComponent(seat)}`;
                
                const card = document.createElement('div');
                card.className = 'bg-slate-900 border border-slate-700 p-3 rounded-lg flex flex-col gap-2';
                
                const canvasId = `qr_canvas_${index}_${Date.now()}`;
                
                card.innerHTML = `
                    <div class="flex items-center gap-3">
                        <div class="bg-white p-1.5 rounded shrink-0">
                            <canvas id="${canvasId}" class="w-20 h-20"></canvas>
                        </div>
                        <div class="overflow-hidden flex-1">
                            <p class="text-xs font-bold text-sky-300">Seat: ${seat}</p>
                            <p class="text-[10px] text-slate-400 truncate mt-0.5">${targetUrl}</p>
                            <a href="${targetUrl}" target="_blank" class="inline-block mt-1 text-[10px] bg-blue-600 hover:bg-blue-500 text-white px-2 py-0.5 rounded">Test Link ↗</a>
                        </div>
                    </div>
                    <div class="flex gap-2 pt-1 border-t border-slate-800">
                        <button onclick="downloadSingleQR('${canvasId}', '${seat}')" class="flex-1 bg-emerald-700 hover:bg-emerald-600 text-white text-[10px] py-1 rounded font-medium">📥 Download QR</button>
                        <button onclick="copySingleQR('${canvasId}')" class="flex-1 bg-slate-700 hover:bg-slate-600 text-white text-[10px] py-1 rounded font-medium">📋 Copy QR</button>
                    </div>
                `;
                container.appendChild(card);

                setTimeout(() => {
                    const canvasElement = document.getElementById(canvasId);
                    if (canvasElement) {
                        QRCode.toCanvas(canvasElement, targetUrl, { width: 120, margin: 1 }, function (error) {
                            if (error) console.error("QR Error:", error);
                        });
                    }
                }, 50);

                generatedData.push({ seat, targetUrl, canvasId });
            });

            if (generatedData.length > 0) {
                document.getElementById('downloadZipBtn').classList.remove('hidden');
            }
        }

        function downloadSingleQR(canvasId, seat) {
            const canvas = document.getElementById(canvasId);
            canvas.toBlob(function(blob) {
                saveAs(blob, `QR_${seat}.png`);
            });
        }

        async function copySingleQR(canvasId) {
            const canvas = document.getElementById(canvasId);
            try {
                canvas.toBlob(async function(blob) {
                    await navigator.clipboard.write([new ClipboardItem({ 'image/png': blob })]);
                    alert("QR Code image copied to clipboard!");
                });
            } catch (err) {
                alert("Failed to copy QR image. Your browser might not support direct image copying.");
            }
        }

        async function downloadAllZip() {
            const zip = new JSZip();
            const folder = zip.folder("Generated_QR_Codes");

            for (let item of generatedData) {
                const canvas = document.getElementById(item.canvasId);
                const dataUrl = canvas.toDataURL("image/png");
                const base64Data = dataUrl.replace(/^data:image\/png;base64,/, "");
                folder.file(`QR_${item.seat}.png`, base64Data, { base64: true });
            }

            const content = await zip.generateAsync({ type: "blob" });
            saveAs(content, "Portal_QRs.zip");
        }
    </script>
</body>
</html>
