# Birthday_gift
A beautiful, multi-page frontend birthday gift project built using HTML5, CSS3, and JavaScript. Includes customized UI components, responsive layouts, love letter interactive animation, and responsive media handling."
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Birthdaygift – A Gift From My Heart ❤️</title>
    <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Montserrat:wght@300;400;500;600&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <link rel="stylesheet" href="style.css">
    <style>
        /* Core Styling & Custom Properties */
.stars-bg {
    background-image: radial-gradient(circle at 10% 20%, #f59e0b 1px, transparent 1px),
                      radial-gradient(circle at 80% 70%, #fbbf24 1px, transparent 1px);
    background-size: 80px 80px;
}

.gold-glow {
    filter: drop-shadow(0 0 15px rgba(251, 191, 36, 0.7));
}

@keyframes pulseSlow {
    0%, 100% { transform: scale(1); opacity: 0.9; }
    50% { transform: scale(1.08); opacity: 1; }
}

.pulse-heart {
    animation: pulseSlow 2.5s infinite ease-in-out;
}

/* Luxury Glass Cards */
.glass-card {
    background: rgba(15, 15, 15, 0.65);
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
}

/* Premium Glow Action Buttons */
.btn-premium {
    background: linear-gradient(135deg, #e11d48 0%, #be123c 100%);
    color: white;
    padding: 0.75rem 2rem;
    border-radius: 9999px;
    font-weight: 500;
    font-size: 0.875rem;
    letter-spacing: 0.05em;
    box-shadow: 0 4px 20px rgba(225, 29, 72, 0.3);
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    cursor: pointer;
}

.btn-premium:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 25px rgba(225, 29, 72, 0.5);
}

/* Countdown Visual Blocks */
.countdown-box {
    background: rgba(20, 20, 20, 0.8);
    border: 1px solid rgba(255, 255, 255, 0.05);
    padding: 1rem;
    border-radius: 1rem;
    min-w: 70px;
}
.countdown-box span {
    display: block;
    font-size: 1.75rem;
    font-weight: 600;
    color: #fda4af;
}
.countdown-box label {
    font-size: 0.65rem;
    color: #71717a;
    text-transform: uppercase;
    letter-spacing: 0.05em;
}

/* Polaroid Photo Frame Design */
.polaroid {
    background: white;
    padding: 12px 12px 24px 12px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.5);
    transform: rotate(var(--tw-rotate, -2deg));
    transition: all 0.4s ease;
    cursor: pointer;
}
.polaroid:nth-child(even) { --tw-rotate: 3deg; }
.polaroid:nth-child(3n) { --tw-rotate: -1.5deg; }
.polaroid:hover {
    transform: scale(1.05) rotate(0deg) translateY(-10px);
    z-index: 10;
    box-shadow: 0 20px 40px rgba(225, 29, 72, 0.2);
}
.polaroid img {
    width: 100%;
    height: 180px;
    object-fit: cover;
    filter: grayscale(20%);
}
.polaroid p {
    font-family: 'Great Vibes', cursive;
    color: #27272a;
    font-size: 1.5rem;
    text-align: center;
    margin-top: 12px;
}

/* Reasons Cards */
.reason-card {
    background: rgba(20, 20, 20, 0.5);
    border: 1px solid rgba(255, 255, 255, 0.03);
    border-radius: 1rem;
    padding: 2rem 1rem;
    text-align: center;
    transition: all 0.3s ease;
}
.reason-card:hover {
    border-color: rgba(244, 63, 94, 0.3);
    background: rgba(244, 63, 94, 0.05);
    transform: translateY(-5px);
}
.reason-card h3 {
    font-size: 0.9rem;
    font-weight: 500;
    color: #e4e4e7;
    margin-top: 0.5rem;
}

/* Realistic Vintage Love Letter Paper */
.letter-paper {
    background: #fdf6e2;
    background-image: linear-gradient(rgba(0,0,0,0.05) 1px, transparent 1px);
    background-size: 100% 2rem;
}

/* Timeline Soft Cards */
.timeline-card {
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.6s ease-out;
}
.timeline-card.visible {
    opacity: 1;
    transform: translateY(0);
}
    </style>
</head>
<body class="bg-black text-white font-['Montserrat'] select-none overflow-x-hidden min-h-screen">

    <audio id="bg-music" loop src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3"></audio>

    <section id="page-1" class="fixed inset-0 bg-black z-50 flex flex-col justify-center items-center p-4">
        <div class="absolute inset-0 opacity-30 stars-bg"></div>
        <div class="relative mb-8 pulse-heart"><i class="fa-solid fa-heart text-amber-400 text-7xl gold-glow"></i></div>
        <div class="text-center h-24 mb-12 flex items-center justify-center">
            <p id="load-text" class="font-['Great_Vibes'] text-amber-300 text-4xl md:text-5xl transition-opacity duration-1000">Every love story has a beautiful beginning...</p>
        </div>
        <div class="w-64 bg-zinc-900 h-[3px] rounded-full overflow-hidden relative border border-zinc-800"><div id="progress-bar" class="h-full bg-gradient-to-r from-amber-500 to-yellow-300 w-0 dynamic-shadow"></div></div>
        <div class="mt-3 text-xs tracking-[0.2em] text-zinc-500 uppercase">Loading... <span id="progress-text">0%</span></div>
    </section>

    <section id="page-2" class="hidden fixed inset-0 bg-black z-40 flex flex-col justify-center items-center p-6 text-center">
        <div class="mb-6 transform hover:scale-110 transition-transform duration-500"><i class="fa-solid fa-box-open text-rose-500 text-8xl"></i></div>
        <h1 class="font-['Great_Vibes'] text-rose-400 text-5xl md:text-6xl mb-4">I Have Something Special For You</h1>
        <p class="text-zinc-400 tracking-wide text-sm mb-8 flex items-center gap-2">Only open if today is your birthday <i class="fa-solid fa-heart text-rose-500"></i></p>
        <button onclick="nextPage(2, 3)" class="btn-premium">Begin Surprise</button>
    </section>

    <section id="page-3" class="hidden fixed inset-0 bg-black z-40 flex flex-col justify-center items-center p-6">
        <div class="glass-card p-8 rounded-2xl w-full max-w-sm text-center border border-zinc-800">
            <i class="fa-solid fa-lock text-rose-500 text-4xl mb-4"></i>
            <h2 class="text-xl tracking-wider mb-6 uppercase">Enter Your Birthday <i class="fa-solid fa-cake-candles"></i></h2>
            <input type="text" id="bday-input" placeholder="DD/MM/YYYY" class="w-full bg-zinc-900 border border-zinc-800 rounded-xl py-3 px-4 text-center tracking-widest text-white font-semibold focus:outline-none focus:border-rose-500 transition-colors mb-4">
            <button onclick="checkPassword()" class="btn-premium w-full">Unlock</button>
            <p id="lock-error" class="text-xs mt-3 font-medium transition-all duration-300 opacity-0"></p>
        </div>
    </section>

    <section id="page-4" class="hidden fixed inset-0 bg-black z-40 flex flex-col justify-center items-center p-6 text-center">
        <h2 class="font-['Great_Vibes'] text-rose-400 text-4xl mb-8">Your Surprise Starts In <i class="fa-solid fa-heart text-rose-500"></i></h2>
        <div class="flex gap-4 mb-8">
            <div class="countdown-box"><span id="cd-days">00</span><label>Days</label></div>
            <div class="countdown-box"><span id="cd-hours">05</span><label>Hours</label></div>
            <div class="countdown-box"><span id="cd-mins">12</span><label>Mins</label></div>
            <div class="countdown-box"><span id="cd-secs">08</span><label>Secs</label></div>
        </div>
        <p class="text-zinc-400 text-sm tracking-widest italic">"Every second brings me closer to celebrating you..."</p>
    </section>

    <main id="main-content" class="hidden relative w-full min-h-screen">
        <section id="page-5" class="min-h-screen flex flex-col justify-center items-center text-center p-6 relative">
            <div class="absolute top-12 right-12 w-28 h-28 rounded-full bg-zinc-200/20 blur-sm shadow-[0_0_50px_rgba(255,255,255,0.2)]"></div>
            <div class="text-6xl mb-4 animate-bounce">🎉</div>
            <h1 class="font-['Great_Vibes'] text-rose-400 text-6xl md:text-7xl mb-6">Happy Birthday My Love ❤️</h1>
            <p id="typewriter" class="text-zinc-300 font-light tracking-wide max-w-md h-12 text-lg"></p>
            <a href="#page-6" class="mt-12 btn-premium inline-block">Continue <i class="fa-solid fa-chevron-down ml-2 text-xs"></i></a>
        </section>

        <section id="page-6" class="min-h-screen py-20 max-w-xl mx-auto px-6 relative">
            <h2 class="text-center font-['Great_Vibes'] text-rose-400 text-5xl mb-16">Our Precious Timeline</h2>
            <div class="relative border-l border-zinc-800 ml-4 space-y-12">
                <div class="relative pl-8 timeline-card">
                    <div class="absolute -left-[9px] top-1 w-4 h-4 rounded-full bg-rose-500 shadow-[0_0_10px_#f43f5e]"></div>
                    <h3 class="font-semibold text-lg text-rose-300">❤️ We Met</h3>
                    <p class="text-zinc-400 text-sm mt-1">A random hi that changed everything perfectly.</p>
                </div>
                <div class="relative pl-8 timeline-card">
                    <div class="absolute -left-[9px] top-1 w-4 h-4 rounded-full bg-rose-500 shadow-[0_0_10px_#f43f5e]"></div>
                    <h3 class="font-semibold text-lg text-rose-300">😊 We Started Talking</h3>
                    <p class="text-zinc-400 text-sm mt-1">Endless conversations, shared secrets, and late-night laughter.</p>
                </div>
                <div class="relative pl-8 timeline-card">
                    <div class="absolute -left-[9px] top-1 w-4 h-4 rounded-full bg-rose-500 shadow-[0_0_10px_#f43f5e]"></div>
                    <h3 class="font-semibold text-lg text-rose-300">💕 We Fell In Love</h3>
                    <p class="text-zinc-400 text-sm mt-1">The magical moment when my heart knew it completely belonged to you.</p>
                </div>
                <div class="relative pl-8 timeline-card">
                    <div class="absolute -left-[9px] top-1 w-4 h-4 rounded-full bg-rose-500 shadow-[0_0_10px_#f43f5e]"></div>
                    <h3 class="font-semibold text-lg text-rose-300">🌍 Long Distance</h3>
                    <p class="text-zinc-400 text-sm mt-1">Miles apart physically, but infinitely closer by soul every single second.</p>
                </div>
                <div class="relative pl-8 timeline-card">
                    <div class="absolute -left-[9px] top-1 w-4 h-4 rounded-full bg-rose-500 shadow-[0_0_10px_#f43f5e]"></div>
                    <h3 class="font-semibold text-lg text-rose-300">❤️ Forever</h3>
                    <p class="text-zinc-400 text-sm mt-1">And this is just the wonderful beginning of our dynamic story...</p>
                </div>
            </div>
        </section>

        <section id="page-7" class="min-h-screen py-20 px-6 max-w-4xl mx-auto">
            <h2 class="text-center font-['Great_Vibes'] text-rose-400 text-5xl mb-6">Our Beautiful Gallery</h2>
            <p class="text-center text-zinc-500 text-xs uppercase tracking-widest mb-12">Click on any photo to zoom</p>
            <div class="grid grid-cols-2 md:grid-cols-3 gap-6">
                <div class="polaroid" onclick="zoomImg(this)"><img src="https://picsum.photos/400/500?random=1" alt="Memory 1"><p>Beautiful Moments</p></div>
                <div class="polaroid" onclick="zoomImg(this)"><img src="https://picsum.photos/400/500?random=2" alt="Memory 2"><p>Your Golden Smile</p></div>
                <div class="polaroid" onclick="zoomImg(this)"><img src="https://picsum.photos/400/500?random=3" alt="Memory 3"><p>Cute Shenanigans</p></div>
                <div class="polaroid" onclick="zoomImg(this)"><img src="https://picsum.photos/400/500?random=4" alt="Memory 4"><p>Holding Hands</p></div>
                <div class="polaroid" onclick="zoomImg(this)"><img src="https://picsum.photos/400/500?random=5" alt="Memory 5"><p>The Deep Eyes</p></div>
                <div class="polaroid" onclick="zoomImg(this)"><img src="https://picsum.photos/400/500?random=6" alt="Memory 6"><p>Together Forever</p></div>
            </div>
        </section>

        <section id="page-8" class="min-h-screen py-20 px-6 max-w-4xl mx-auto">
            <h2 class="text-center font-['Great_Vibes'] text-rose-400 text-5xl mb-12">Reasons I Love You ❤️</h2>
            <div class="grid grid-cols-2 md:grid-cols-3 gap-6">
                <div class="reason-card"><i class="fa-regular fa-face-smile text-rose-400 text-3xl mb-3"></i><h3>Your Smile</h3></div>
                <div class="reason-card"><i class="fa-regular fa-heart text-rose-400 text-3xl mb-3"></i><h3>Your Care</h3></div>
                <div class="reason-card"><i class="fa-solid fa-microphone-lines text-rose-400 text-3xl mb-3"></i><h3>Your Voice</h3></div>
                <div class="reason-card"><i class="fa-solid fa-hand-holding-heart text-rose-400 text-3xl mb-3"></i><h3>Your Kindness</h3></div>
                <div class="reason-card"><i class="fa-solid fa-hands-holding text-rose-400 text-3xl mb-3"></i><h3>Your Support</h3></div>
                <div class="reason-card"><i class="fa-solid fa-infinity text-rose-400 text-3xl mb-3"></i><h3>Everything About You</h3></div>
            </div>
        </section>

        <section id="page-9" class="min-h-screen flex flex-col justify-center items-center text-center p-6 bg-zinc-950/40">
            <h2 class="font-['Great_Vibes'] text-rose-400 text-5xl mb-8">A Special Gift For You ❤️</h2>
            <div id="gift-box" onclick="explodeGift()" class="text-9xl cursor-pointer hover:scale-110 transition-transform duration-300 drop-shadow-[0_0_30px_rgba(244,63,94,0.4)]">🎁</div>
            <p id="gift-hint" class="mt-8 text-xs text-rose-400/60 uppercase tracking-widest animate-pulse">Tap To Open</p>
        </section>

        <section id="page-10" class="min-h-screen flex flex-col justify-center items-center p-6">
            <div class="letter-paper p-8 md:p-12 rounded-lg max-w-xl shadow-2xl relative border border-amber-900/20 text-amber-950">
                <h2 class="font-['Great_Vibes'] text-3xl border-b border-amber-800/20 pb-2 mb-4">A Letter For You ❤️</h2>
                <p class="font-serif leading-relaxed text-sm space-y-4">
                    Dear Love,<br><br>
                    Happy Birthday to the most amazing person in my entire life. You mean the absolute world to me. Thank you for coming into my life and making it so beautiful.<br><br>
                    I love you more than words can ever express. Every moment spent thinking of you brings immense joy to my soul.
                </p>
                <div class="mt-8 text-right font-['Great_Vibes'] text-2xl">— Yours Forever</div>
            </div>
        </section>

        <section id="page-11" class="min-h-screen flex flex-col justify-center items-center text-center p-6">
            <h2 class="font-['Great_Vibes'] text-rose-400 text-5xl mb-8">Make A Wish ❤️</h2>
            <div class="relative inline-block mb-12">
                <div id="candle-flame" class="absolute left-1/2 -top-6 -translate-x-1/2 w-4 h-6 bg-amber-400 rounded-full blur-[2px] animate-pulse shadow-[0_0_15px_#fbbf24]"></div>
                <div class="text-8xl">🎂</div>
            </div>
            <button id="blow-btn" onclick="blowCandle()" class="btn-premium">Blow Candle 🎂</button>
        </section>

        <section id="page-12" class="min-h-screen flex flex-col justify-center items-center text-center p-6 relative">
            <div class="max-w-md p-8 rounded-3xl border border-rose-500/30 bg-gradient-to-b from-rose-950/20 to-black shadow-[0_0_50px_rgba(244,63,94,0.1)]">
                <p class="text-zinc-300 italic mb-4">"No matter how many miles separate us... My heart will always find you."</p>
                <h2 class="font-['Great_Vibes'] text-rose-400 text-6xl my-6">I Love You ❤️</h2>
                <button onclick="document.getElementById('page-13').scrollIntoView({behavior: 'smooth'})" class="btn-premium px-8">Forever ♾️</button>
            </div>
        </section>

        <section id="page-13" class="min-h-screen flex flex-col justify-center items-center text-center p-6 relative bg-gradient-to-t from-zinc-950 to-black">
            <div class="w-32 h-32 rounded-full bg-zinc-200/10 blur-sm absolute top-20 shadow-[0_0_60px_rgba(255,255,255,0.15)]"></div>
            <p class="text-zinc-400 tracking-widest uppercase text-xs mb-4">Thank you for being the best part of my life.</p>
            <h1 class="font-['Great_Vibes'] text-rose-400 text-6xl mb-12">Happy Birthday</h1>
            <div class="text-xs text-zinc-600 tracking-wider">
                Made with <i class="fa-solid fa-heart text-rose-600 animate-pulse"></i> by Your Love
            </div>
        </section>
    </main>

    <div id="lightbox" onclick="this.classList.add('hidden');" class="hidden fixed inset-0 bg-black/95 z-50 flex justify-center items-center p-4">
        <img id="lightbox-img" class="max-w-full max-h-full rounded-lg shadow-2xl transform scale-95 transition-transform duration-300">
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", () => {
    runLoader();
    setupTimelineScroll();
});

// 1. Loader Logic (Page 1)
function runLoader() {
    const bar = document.getElementById("progress-bar");
    const txt = document.getElementById("progress-text");
    const label = document.getElementById("load-text");
    let val = 0;

    setTimeout(() => {
        label.innerText = "Tonight is all about you...";
    }, 2500);

    const timer = setInterval(() => {
        val += Math.floor(Math.random() * 4) + 1;
        if (val >= 100) {
            val = 100;
            clearInterval(timer);
            setTimeout(() => {
                document.getElementById("page-1").style.opacity = "0";
                setTimeout(() => {
                    document.getElementById("page-1").classList.add("hidden");
                    document.getElementById("page-2").classList.remove("hidden");
                }, 1000);
            }, 500);
        }
        bar.style.width = val + "%";
        txt.innerText = val + "%";
    }, 120);
}

// Global Transition Controller
function nextPage(current, next) {
    document.getElementById(`page-${current}`).classList.add("hidden");
    document.getElementById(`page-${next}`).classList.remove("hidden");
}

// 2. Lock Verification (Page 3)
function checkPassword() {
    const input = document.getElementById("bday-input").value.trim();
    const errorEl = document.getElementById("lock-error");

    // Yahan aap apni true target date match kar sakte hain
    if(input === "14/07/2002" || input === "14/07") { 
        errorEl.className = "text-xs mt-3 font-medium text-emerald-400 opacity-1";
        errorEl.innerText = "❤️ Welcome My Love";

        // Start background ambient music safely
        const audio = document.getElementById("bg-music");
        audio.play().catch(e => console.log("Audio block active"));

        setTimeout(() => {
            document.getElementById("page-3").classList.add("hidden");
            unlockDashboard();
        }, 1200);
    } else {
        errorEl.className = "text-xs mt-3 font-medium text-rose-500 opacity-1";
        errorEl.innerText = "❌ Incorrect date! Try again.";
    }
}

// Unlocks dashboard content
function unlockDashboard() {
    const main = document.getElementById("main-content");
    main.classList.remove("hidden");
    startTypewriter();
}

// 3. Typewriter Engine (Page 5)
function startTypewriter() {
    const text = "You are the most beautiful chapter of my life...";
    const el = document.getElementById("typewriter");
    let idx = 0;

    function type() {
        if(idx < text.length) {
            el.innerHTML += text.charAt(idx);
            idx++;
            setTimeout(type, 80);
        }
    }
    type();
}

// 4. Timeline Intersection Observer (Page 6)
function setupTimelineScroll() {
    const cards = document.querySelectorAll('.timeline-card');
    const obs = new IntersectionObserver(entries => {
        entries.forEach(e => {
            if(e.isIntersecting) {
                e.target.classList.add('visible');
            }
        });
    }, { threshold: 0.2 });
    cards.forEach(c => obs.observe(c));
}

// 5. Image Lightbox System (Page 7)
function zoomImg(card) {
    const src = card.querySelector('img').src;
    const box = document.getElementById("lightbox");
    const img = document.getElementById("lightbox-img");
    img.src = src;
    box.classList.remove("hidden");
}

// 6. Gift Explode Event (Page 9)
function explodeGift() {
    const box = document.getElementById("gift-box");
    const hint = document.getElementById("gift-hint");
    box.innerText = "💥";
    hint.innerText = "Surprise Opened! 🎉";

    confetti({ particleCount: 150, spread: 80, origin: { y: 0.6 } });

    setTimeout(() => {
        box.innerText = "💖";
        box.style.transform = "scale(1.3)";
    }, 600);
}

// 7. Candle Interactivity (Page 11)
function blowCandle() {
    const flame = document.getElementById("candle-flame");
    const btn = document.getElementById("blow-btn");
    flame.style.display = "none";
    btn.innerText = "Wish Made! ✨";

    // Continuous festive bursts
    let duration = 3 * 1000;
    let end = Date.now() + duration;

    (function frame() {
    confetti({ particleCount: 3, angle: 60, spread: 55, origin: { x: 0 } });
    confetti({ particleCount: 3, angle: 120, spread: 55, origin: { x: 1 } });
    if (Date.now() < end) requestAnimationFrame(frame);
    }());
}
    </script>
</body>
</html>
