<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Encargo Hats</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Barlow+Condensed:wght@300;400;600;700;900&family=Barlow:wght@300;400;500&display=swap" rel="stylesheet"/>
<style>
  :root {
    --red: #8b0000;
    --red-bright: #c0000a;
    --red-glow: rgba(139,0,0,0.5);
    --white: #f0ece8;
    --off: #1a1a1a;
    --dark: #0a0a0a;
    --mid: #111;
  }

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

html { scroll-behavior: smooth; }

body {
background: var(–dark);
color: var(–white);
font-family: ‘Barlow’, sans-serif;
overflow-x: hidden;
cursor: default;
}

/* ── NOISE OVERLAY ── */
body::before {
content: ‘’;
position: fixed;
inset: 0;
background-image: url(“data:image/svg+xml,%3Csvg viewBox=‘0 0 512 512’ xmlns=‘http://www.w3.org/2000/svg’%3E%3Cfilter id=‘n’%3E%3CfeTurbulence type=‘fractalNoise’ baseFrequency=‘0.75’ numOctaves=‘4’ stitchTiles=‘stitch’/%3E%3C/filter%3E%3Crect width=‘100%25’ height=‘100%25’ filter=‘url(%23n)’ opacity=‘1’/%3E%3C/svg%3E”);
opacity: 0.035;
pointer-events: none;
z-index: 9999;
}

/* ── NAV ── */
nav {
position: fixed;
top: 0; left: 0; right: 0;
z-index: 100;
display: flex;
align-items: center;
justify-content: space-between;
padding: 20px 48px;
background: linear-gradient(to bottom, rgba(0,0,0,0.95) 0%, transparent 100%);
transition: background 0.4s;
}
nav.scrolled {
background: rgba(5,5,5,0.97);
border-bottom: 1px solid rgba(139,0,0,0.2);
backdrop-filter: blur(12px);
}
.nav-logo {
display: flex;
align-items: center;
gap: 12px;
text-decoration: none;
}
.nav-logo img {
width: 42px;
height: 42px;
object-fit: contain;
filter: drop-shadow(0 0 8px rgba(139,0,0,0.6));
}
.nav-logo-text {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 22px;
letter-spacing: 3px;
color: var(–white);
}
.nav-links {
display: flex;
gap: 40px;
list-style: none;
}
.nav-links a {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 13px;
font-weight: 600;
letter-spacing: 3px;
text-transform: uppercase;
color: rgba(240,236,232,0.6);
text-decoration: none;
transition: color 0.2s;
position: relative;
}
.nav-links a::after {
content: ‘’;
position: absolute;
bottom: -4px; left: 0;
width: 0; height: 1px;
background: var(–red-bright);
transition: width 0.3s;
}
.nav-links a:hover { color: var(–white); }
.nav-links a:hover::after { width: 100%; }
.nav-cta {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 12px;
font-weight: 700;
letter-spacing: 3px;
text-transform: uppercase;
color: var(–white);
background: var(–red);
border: none;
padding: 10px 24px;
cursor: pointer;
transition: background 0.2s, box-shadow 0.2s;
text-decoration: none;
}
.nav-cta:hover {
background: var(–red-bright);
box-shadow: 0 0 20px var(–red-glow);
}

/* ── HERO ── */
#hero {
min-height: 100vh;
display: flex;
align-items: center;
justify-content: center;
position: relative;
overflow: hidden;
padding: 120px 48px 80px;
}
.hero-grid-bg {
position: absolute;
inset: 0;
background-image:
linear-gradient(rgba(139,0,0,0.06) 1px, transparent 1px),
linear-gradient(90deg, rgba(139,0,0,0.06) 1px, transparent 1px);
background-size: 60px 60px;
}
.hero-glow {
position: absolute;
top: 50%; left: 50%;
transform: translate(-50%, -50%);
width: 700px; height: 700px;
background: radial-gradient(circle, rgba(139,0,0,0.18) 0%, transparent 65%);
border-radius: 50%;
pointer-events: none;
}
.hero-content {
position: relative;
z-index: 2;
text-align: center;
max-width: 900px;
}
.hero-eyebrow {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 12px;
letter-spacing: 8px;
color: var(–red-bright);
text-transform: uppercase;
margin-bottom: 24px;
opacity: 0;
animation: fadeUp 0.8s 0.2s forwards;
}
.hero-logo-img {
width: 160px;
height: 160px;
object-fit: contain;
filter: drop-shadow(0 0 40px rgba(139,0,0,0.7)) drop-shadow(0 0 80px rgba(139,0,0,0.3));
margin-bottom: 32px;
opacity: 0;
animation: fadeUp 0.9s 0.4s forwards;
}
.hero-title {
font-family: ‘Bebas Neue’, sans-serif;
font-size: clamp(72px, 12vw, 160px);
line-height: 0.9;
letter-spacing: 4px;
color: var(–white);
text-shadow: 0 0 80px rgba(139,0,0,0.3);
opacity: 0;
animation: fadeUp 0.9s 0.5s forwards;
}
.hero-title span {
color: var(–red-bright);
display: block;
}
.hero-subtitle {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 16px;
letter-spacing: 10px;
color: rgba(240,236,232,0.4);
text-transform: uppercase;
margin-top: 16px;
opacity: 0;
animation: fadeUp 0.9s 0.7s forwards;
}
.hero-actions {
display: flex;
gap: 16px;
justify-content: center;
margin-top: 48px;
opacity: 0;
animation: fadeUp 0.9s 0.9s forwards;
}
.btn-primary {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 13px;
font-weight: 700;
letter-spacing: 4px;
text-transform: uppercase;
color: var(–white);
background: var(–red);
border: none;
padding: 16px 40px;
cursor: pointer;
transition: all 0.25s;
text-decoration: none;
display: inline-block;
}
.btn-primary:hover {
background: var(–red-bright);
box-shadow: 0 0 30px var(–red-glow), 0 0 60px rgba(139,0,0,0.2);
transform: translateY(-2px);
}
.btn-outline {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 13px;
font-weight: 700;
letter-spacing: 4px;
text-transform: uppercase;
color: var(–white);
background: transparent;
border: 1px solid rgba(240,236,232,0.25);
padding: 16px 40px;
cursor: pointer;
transition: all 0.25s;
text-decoration: none;
display: inline-block;
}
.btn-outline:hover {
border-color: var(–red-bright);
color: var(–red-bright);
box-shadow: 0 0 20px rgba(139,0,0,0.2);
transform: translateY(-2px);
}
.hero-scroll {
position: absolute;
bottom: 36px;
left: 50%;
transform: translateX(-50%);
display: flex;
flex-direction: column;
align-items: center;
gap: 8px;
opacity: 0;
animation: fadeIn 1s 1.4s forwards;
}
.hero-scroll span {
font-size: 9px;
letter-spacing: 4px;
color: rgba(240,236,232,0.3);
text-transform: uppercase;
}
.scroll-line {
width: 1px;
height: 40px;
background: linear-gradient(to bottom, rgba(139,0,0,0.8), transparent);
animation: scrollPulse 2s ease-in-out infinite;
}

/* ── MARQUEE ── */
.marquee-strip {
background: var(–red);
overflow: hidden;
padding: 14px 0;
position: relative;
}
.marquee-track {
display: flex;
gap: 0;
white-space: nowrap;
animation: marquee 20s linear infinite;
}
.marquee-item {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 15px;
letter-spacing: 4px;
color: rgba(255,255,255,0.85);
padding: 0 36px;
flex-shrink: 0;
}
.marquee-dot {
color: rgba(255,255,255,0.4);
}

/* ── SECTION BASE ── */
section {
padding: 100px 48px;
}
.section-label {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 11px;
letter-spacing: 6px;
color: var(–red-bright);
text-transform: uppercase;
margin-bottom: 16px;
}
.section-title {
font-family: ‘Bebas Neue’, sans-serif;
font-size: clamp(48px, 7vw, 88px);
line-height: 0.95;
letter-spacing: 2px;
color: var(–white);
margin-bottom: 32px;
}
.divider {
width: 48px;
height: 2px;
background: var(–red);
margin-bottom: 32px;
}

/* ── SHOP ── */
#shop { background: var(–mid); }
.shop-header {
display: flex;
align-items: flex-end;
justify-content: space-between;
margin-bottom: 56px;
flex-wrap: wrap;
gap: 24px;
}
.shop-grid {
display: grid;
grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
gap: 2px;
}
.product-card {
background: var(–off);
position: relative;
overflow: hidden;
cursor: pointer;
group: true;
}
.product-img {
width: 100%;
aspect-ratio: 1;
background: #181818;
display: flex;
align-items: center;
justify-content: center;
position: relative;
overflow: hidden;
transition: transform 0.4s ease;
}
.product-card:hover .product-img {
transform: scale(1.03);
}
.product-img-inner {
width: 55%;
height: 55%;
display: flex;
align-items: center;
justify-content: center;
position: relative;
}
.product-img-inner img {
width: 100%;
height: 100%;
object-fit: contain;
filter: drop-shadow(0 4px 20px rgba(0,0,0,0.6));
transition: filter 0.3s, transform 0.3s;
}
.product-card:hover .product-img-inner img {
filter: drop-shadow(0 0 20px rgba(139,0,0,0.5)) drop-shadow(0 4px 20px rgba(0,0,0,0.6));
transform: translateY(-4px);
}
.product-badge {
position: absolute;
top: 16px; left: 16px;
background: var(–red);
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 10px;
font-weight: 700;
letter-spacing: 3px;
color: #fff;
padding: 4px 10px;
text-transform: uppercase;
}
/* Hat silhouettes using CSS */
.hat-silhouette {
position: absolute;
inset: 0;
display: flex;
align-items: center;
justify-content: center;
}
.hat-bg-snapback {
background: linear-gradient(160deg, #2a2a2a, #181818);
border-radius: 4px;
}
.hat-bg-fitted {
background: linear-gradient(160deg, #1f1f1f, #141414);
}
.hat-bg-dad {
background: linear-gradient(160deg, #252020, #1a1515);
}
.product-overlay {
position: absolute;
inset: 0;
background: linear-gradient(to top, rgba(139,0,0,0.15) 0%, transparent 50%);
opacity: 0;
transition: opacity 0.3s;
}
.product-card:hover .product-overlay { opacity: 1; }
.product-info {
padding: 20px 24px 24px;
border-top: 1px solid rgba(255,255,255,0.04);
}
.product-name {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 18px;
font-weight: 700;
letter-spacing: 2px;
text-transform: uppercase;
color: var(–white);
margin-bottom: 4px;
}
.product-sub {
font-size: 12px;
color: rgba(240,236,232,0.4);
letter-spacing: 1px;
margin-bottom: 16px;
}
.product-footer {
display: flex;
align-items: center;
justify-content: space-between;
}
.product-price {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 26px;
color: var(–white);
letter-spacing: 1px;
}
.product-btn {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 11px;
font-weight: 700;
letter-spacing: 3px;
text-transform: uppercase;
background: var(–red);
color: #fff;
border: none;
padding: 9px 18px;
cursor: pointer;
transition: background 0.2s, box-shadow 0.2s;
}
.product-btn:hover {
background: var(–red-bright);
box-shadow: 0 0 16px var(–red-glow);
}

/* ── ABOUT ── */
#about {
background: var(–dark);
position: relative;
overflow: hidden;
}
.about-grid {
display: grid;
grid-template-columns: 1fr 1fr;
gap: 80px;
align-items: center;
max-width: 1200px;
margin: 0 auto;
}
.about-visual {
position: relative;
display: flex;
align-items: center;
justify-content: center;
}
.about-logo-wrap {
position: relative;
width: 320px;
height: 320px;
display: flex;
align-items: center;
justify-content: center;
}
.about-ring {
position: absolute;
inset: 0;
border: 1px solid rgba(139,0,0,0.2);
border-radius: 50%;
animation: spin 20s linear infinite;
}
.about-ring-2 {
position: absolute;
inset: 20px;
border: 1px dashed rgba(139,0,0,0.12);
border-radius: 50%;
animation: spin 30s linear infinite reverse;
}
.about-glow-bg {
position: absolute;
inset: 40px;
background: radial-gradient(circle, rgba(139,0,0,0.15) 0%, transparent 70%);
border-radius: 50%;
}
.about-logo-img {
width: 180px;
height: 180px;
object-fit: contain;
position: relative;
z-index: 2;
filter: drop-shadow(0 0 30px rgba(139,0,0,0.5));
}
.about-text { position: relative; }
.about-body {
font-size: 16px;
line-height: 1.9;
color: rgba(240,236,232,0.65);
margin-bottom: 24px;
font-weight: 300;
}
.about-stats {
display: grid;
grid-template-columns: repeat(3, 1fr);
gap: 24px;
margin-top: 48px;
padding-top: 40px;
border-top: 1px solid rgba(255,255,255,0.06);
}
.stat-num {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 52px;
color: var(–red-bright);
line-height: 1;
letter-spacing: 2px;
}
.stat-label {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 11px;
letter-spacing: 3px;
color: rgba(240,236,232,0.4);
text-transform: uppercase;
margin-top: 4px;
}

/* ── CONTACT ── */
#contact {
background: var(–mid);
position: relative;
overflow: hidden;
}
#contact::before {
content: ‘EH’;
position: absolute;
right: -40px; bottom: -80px;
font-family: ‘Bebas Neue’, sans-serif;
font-size: 400px;
color: rgba(139,0,0,0.04);
line-height: 1;
pointer-events: none;
user-select: none;
}
.contact-grid {
display: grid;
grid-template-columns: 1fr 1fr;
gap: 80px;
max-width: 1200px;
margin: 0 auto;
align-items: start;
}
.contact-info { position: relative; z-index: 2; }
.contact-body {
font-size: 16px;
line-height: 1.9;
color: rgba(240,236,232,0.55);
margin-bottom: 40px;
font-weight: 300;
max-width: 380px;
}
.contact-item {
display: flex;
align-items: flex-start;
gap: 16px;
margin-bottom: 24px;
}
.contact-icon {
width: 36px;
height: 36px;
background: rgba(139,0,0,0.2);
display: flex;
align-items: center;
justify-content: center;
flex-shrink: 0;
font-size: 16px;
}
.contact-item-label {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 10px;
letter-spacing: 3px;
color: var(–red-bright);
text-transform: uppercase;
margin-bottom: 2px;
}
.contact-item-val {
font-size: 15px;
color: rgba(240,236,232,0.7);
}
.contact-form { position: relative; z-index: 2; }
.form-group { margin-bottom: 20px; }
.form-label {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 11px;
letter-spacing: 3px;
color: rgba(240,236,232,0.4);
text-transform: uppercase;
display: block;
margin-bottom: 8px;
}
.form-input, .form-select, .form-textarea {
width: 100%;
background: rgba(255,255,255,0.04);
border: 1px solid rgba(255,255,255,0.08);
color: var(–white);
font-family: ‘Barlow’, sans-serif;
font-size: 15px;
padding: 14px 18px;
outline: none;
transition: border-color 0.2s, box-shadow 0.2s;
appearance: none;
}
.form-input:focus, .form-select:focus, .form-textarea:focus {
border-color: rgba(139,0,0,0.6);
box-shadow: 0 0 0 3px rgba(139,0,0,0.1);
}
.form-input::placeholder, .form-textarea::placeholder {
color: rgba(240,236,232,0.2);
}
.form-select option { background: #1a1a1a; }
.form-textarea { resize: vertical; min-height: 120px; }
.form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
.form-submit {
width: 100%;
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 13px;
font-weight: 700;
letter-spacing: 5px;
text-transform: uppercase;
color: #fff;
background: var(–red);
border: none;
padding: 18px;
cursor: pointer;
transition: all 0.25s;
margin-top: 8px;
}
.form-submit:hover {
background: var(–red-bright);
box-shadow: 0 0 30px var(–red-glow);
}
.form-note {
font-size: 12px;
color: rgba(240,236,232,0.25);
text-align: center;
margin-top: 12px;
letter-spacing: 1px;
}
.success-msg {
display: none;
background: rgba(139,0,0,0.15);
border: 1px solid rgba(139,0,0,0.4);
padding: 16px 20px;
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 14px;
letter-spacing: 2px;
color: var(–red-bright);
text-transform: uppercase;
margin-top: 16px;
text-align: center;
}

/* ── FOOTER ── */
footer {
background: #040404;
border-top: 1px solid rgba(139,0,0,0.15);
padding: 56px 48px 36px;
}
.footer-top {
display: flex;
justify-content: space-between;
align-items: flex-start;
margin-bottom: 48px;
flex-wrap: wrap;
gap: 40px;
}
.footer-brand { max-width: 280px; }
.footer-logo {
display: flex;
align-items: center;
gap: 12px;
margin-bottom: 16px;
}
.footer-logo img {
width: 36px;
height: 36px;
object-fit: contain;
filter: drop-shadow(0 0 6px rgba(139,0,0,0.5));
}
.footer-logo-text {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 20px;
letter-spacing: 3px;
}
.footer-tagline {
font-size: 13px;
color: rgba(240,236,232,0.3);
line-height: 1.7;
font-weight: 300;
}
.footer-links-group h4 {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 11px;
letter-spacing: 4px;
color: var(–red-bright);
text-transform: uppercase;
margin-bottom: 16px;
}
.footer-links-group ul { list-style: none; }
.footer-links-group li { margin-bottom: 10px; }
.footer-links-group a {
font-size: 14px;
color: rgba(240,236,232,0.45);
text-decoration: none;
transition: color 0.2s;
letter-spacing: 0.5px;
}
.footer-links-group a:hover { color: var(–white); }
.footer-bottom {
border-top: 1px solid rgba(255,255,255,0.05);
padding-top: 28px;
display: flex;
justify-content: space-between;
align-items: center;
flex-wrap: wrap;
gap: 12px;
}
.footer-copy {
font-size: 12px;
color: rgba(240,236,232,0.2);
letter-spacing: 1px;
}
.footer-socials {
display: flex;
gap: 16px;
}
.social-link {
width: 34px; height: 34px;
border: 1px solid rgba(255,255,255,0.08);
display: flex;
align-items: center;
justify-content: center;
font-size: 14px;
color: rgba(240,236,232,0.4);
text-decoration: none;
transition: all 0.2s;
cursor: pointer;
}
.social-link:hover {
border-color: var(–red);
color: var(–red-bright);
box-shadow: 0 0 12px rgba(139,0,0,0.3);
}

/* ── ANIMATIONS ── */
@keyframes fadeUp {
from { opacity: 0; transform: translateY(24px); }
to   { opacity: 1; transform: translateY(0); }
}
@keyframes fadeIn {
from { opacity: 0; }
to   { opacity: 1; }
}
@keyframes marquee {
from { transform: translateX(0); }
to   { transform: translateX(-50%); }
}
@keyframes spin {
from { transform: rotate(0deg); }
to   { transform: rotate(360deg); }
}
@keyframes scrollPulse {
0%, 100% { opacity: 0.3; transform: scaleY(1); }
50%       { opacity: 0.8; transform: scaleY(1.1); }
}

/* ── RESPONSIVE ── */
@media (max-width: 900px) {
nav { padding: 16px 24px; }
.nav-links { display: none; }
section { padding: 72px 24px; }
#hero { padding: 100px 24px 60px; }
.about-grid, .contact-grid { grid-template-columns: 1fr; gap: 48px; }
.about-logo-wrap { width: 220px; height: 220px; }
.about-logo-img { width: 120px; height: 120px; }
.form-row { grid-template-columns: 1fr; }
footer { padding: 48px 24px 28px; }
.footer-top { flex-direction: column; gap: 32px; }
.about-visual { order: -1; }
}

/* ── PASSWORD SCREEN ── */
#password-screen {
position: fixed;
inset: 0;
background: #050505;
z-index: 99999;
display: flex;
align-items: center;
justify-content: center;
}
#password-screen .pw-grid {
position: absolute;
inset: 0;
background-image:
linear-gradient(rgba(139,0,0,0.05) 1px, transparent 1px),
linear-gradient(90deg, rgba(139,0,0,0.05) 1px, transparent 1px);
background-size: 60px 60px;
}
#password-screen .pw-glow {
position: absolute;
top: 50%; left: 50%;
transform: translate(-50%, -50%);
width: 600px; height: 600px;
background: radial-gradient(circle, rgba(139,0,0,0.12) 0%, transparent 65%);
border-radius: 50%;
pointer-events: none;
}
#password-screen .pw-box {
position: relative;
z-index: 2;
text-align: center;
width: 100%;
max-width: 420px;
padding: 0 32px;
}
#password-screen .pw-logo {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 80px;
line-height: 1;
text-shadow: 0 0 40px rgba(139,0,0,0.7);
margin-bottom: 8px;
}
#password-screen .pw-brand {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 12px;
letter-spacing: 8px;
color: rgba(240,236,232,0.35);
text-transform: uppercase;
margin-bottom: 48px;
}
#password-screen .pw-label {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 11px;
letter-spacing: 4px;
color: rgba(240,236,232,0.35);
text-transform: uppercase;
margin-bottom: 12px;
}
#password-screen .pw-input {
width: 100%;
background: rgba(255,255,255,0.04);
border: 1px solid rgba(255,255,255,0.1);
color: #f0ece8;
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 18px;
letter-spacing: 4px;
padding: 16px 20px;
text-align: center;
outline: none;
transition: border-color 0.2s, box-shadow 0.2s;
}
#password-screen .pw-input:focus {
border-color: rgba(139,0,0,0.6);
box-shadow: 0 0 0 3px rgba(139,0,0,0.1);
}
#password-screen .pw-input.shake {
animation: pwshake 0.4s ease;
border-color: rgba(192,0,10,0.8);
}
#password-screen .pw-btn {
width: 100%;
margin-top: 12px;
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 13px;
font-weight: 700;
letter-spacing: 5px;
text-transform: uppercase;
color: #fff;
background: #8b0000;
border: none;
padding: 16px;
cursor: pointer;
transition: all 0.25s;
}
#password-screen .pw-btn:hover {
background: #c0000a;
box-shadow: 0 0 30px rgba(139,0,0,0.5);
}
#password-screen .pw-error {
margin-top: 14px;
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 12px;
letter-spacing: 3px;
color: #c0000a;
text-transform: uppercase;
min-height: 20px;
}
#password-screen.hidden {
animation: pwfadeout 0.6s forwards;
pointer-events: none;
}
@keyframes pwshake {
0%,100% { transform: translateX(0); }
20% { transform: translateX(-10px); }
40% { transform: translateX(10px); }
60% { transform: translateX(-6px); }
80% { transform: translateX(6px); }
}
@keyframes pwfadeout {
from { opacity: 1; }
to   { opacity: 0; }
}
</style>

</head>
<body>
<!-- PASSWORD SCREEN -->
<div id="password-screen">
  <div class="pw-grid"></div>
  <div class="pw-glow"></div>
  <div class="pw-box">
    <div class="pw-logo">E<span style="color:#c0000a;font-size:56px;vertical-align:middle;">⚡</span>H</div>
    <div class="pw-brand">Encargo Hats</div>
    <div class="pw-label">Enter Password</div>
    <input type="password" class="pw-input" id="pw-input" placeholder="••••••••" onkeydown="if(event.key==='Enter')checkPW()"/>
    <button class="pw-btn" onclick="checkPW()">⚡ Enter</button>
    <div class="pw-error" id="pw-error"></div>
  </div>
</div>
<script>
  function checkPW() {
    const input = document.getElementById('pw-input');
    const error = document.getElementById('pw-error');
    if (input.value === 'Ruta2026') {
      const screen = document.getElementById('password-screen');
      screen.classList.add('hidden');
      setTimeout(() => screen.remove(), 700);
    } else {
      error.textContent = 'Wrong password. Try again.';
      input.classList.remove('shake');
      void input.offsetWidth;
      input.classList.add('shake');
      input.value = '';
      setTimeout(() => { error.textContent = ''; input.classList.remove('shake'); }, 2000);
    }
  }
</script>

<!-- NAV -->

<nav id="navbar">
  <a href="#hero" class="nav-logo">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/Camponotus_flavomarginatus_ant.jpg/320px-Camponotus_flavomarginatus_ant.jpg" alt="EH" id="nav-logo-img" style="display:none"/>
    <span style="font-family:'Bebas Neue',sans-serif;font-size:28px;color:#f0ece8;letter-spacing:2px;">E<span style="color:#c0000a">⚡</span>H</span>
    <span class="nav-logo-text" style="font-size:16px;color:rgba(240,236,232,0.5);letter-spacing:2px;font-family:'Barlow Condensed',sans-serif;font-weight:300;">ENCARGO HATS</span>
  </a>
  <ul class="nav-links">
    <li><a href="#shop">Shop</a></li>
    <li><a href="#about">About</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <a href="#contact" class="nav-cta">Custom Order</a>
</nav>

<!-- HERO -->

<section id="hero">
  <div class="hero-grid-bg"></div>
  <div class="hero-glow"></div>
  <!-- BG graffiti words -->
  <div style="position:absolute;inset:0;overflow:hidden;pointer-events:none;">
    <div style="position:absolute;font-family:'Bebas Neue',sans-serif;font-size:180px;color:rgba(139,0,0,0.04);top:-20px;left:-40px;letter-spacing:8px;line-height:1;">ENCARGO</div>
    <div style="position:absolute;font-family:'Bebas Neue',sans-serif;font-size:280px;color:rgba(139,0,0,0.03);bottom:-60px;right:-60px;letter-spacing:4px;line-height:1;">EH</div>
  </div>
  <div class="hero-content">
    <div class="hero-eyebrow">⚡ Premium Headwear</div>
    <!-- EH logo using CSS since we reference the uploaded image path -->
    <div class="hero-logo-img" style="width:160px;height:160px;margin:0 auto 32px;display:flex;align-items:center;justify-content:center;position:relative;opacity:0;animation:fadeUp 0.9s 0.4s forwards;">
      <div style="position:absolute;inset:-20px;background:radial-gradient(circle,rgba(139,0,0,0.35) 0%,transparent 70%);border-radius:50%;filter:blur(16px);"></div>
      <div style="font-family:'Bebas Neue',sans-serif;font-size:120px;line-height:1;position:relative;z-index:2;text-shadow:0 0 40px rgba(139,0,0,0.8);">E<span style="color:#c0000a;font-size:80px;vertical-align:middle;text-shadow:0 0 30px rgba(192,0,10,0.9);">⚡</span>H</div>
    </div>
    <div class="hero-title">ENCARGO<span>HATS</span></div>
    <div class="hero-subtitle">H E A D W E A R &nbsp;&nbsp; C U L T U R E</div>
    <div class="hero-actions">
      <a href="#shop" class="btn-primary">Shop Now</a>
      <a href="#contact" class="btn-outline">Custom Order</a>
    </div>
  </div>
  <div class="hero-scroll">
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<!-- MARQUEE -->

<div class="marquee-strip">
  <div class="marquee-track" id="marquee">
    <span class="marquee-item">Snapbacks <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Fitted Caps <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Dad Hats <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Custom Orders <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Limited Drops <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Encargo Hats <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Snapbacks <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Fitted Caps <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Dad Hats <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Custom Orders <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Limited Drops <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Encargo Hats <span class="marquee-dot">✦</span></span>
  </div>
</div>

<!-- SHOP -->

<section id="shop">
  <div class="shop-header">
    <div>
      <div class="section-label">/ 01 — Collection</div>
      <div class="section-title">THE<br>DROP</div>
      <div class="divider"></div>
    </div>
    <p style="max-width:320px;font-size:15px;color:rgba(240,236,232,0.5);line-height:1.8;font-weight:300;">Every piece is built for the streets. Bold designs, quality materials, limited runs.</p>
  </div>
  <div class="shop-grid">

```
<!-- Product 1 -->
<div class="product-card">
  <div class="product-img hat-bg-snapback">
    <div class="product-img-inner">
      <div style="font-family:'Bebas Neue',sans-serif;font-size:80px;line-height:1;text-shadow:0 0 30px rgba(139,0,0,0.7);">E<span style="color:#c0000a;font-size:56px;vertical-align:middle;">⚡</span>H</div>
    </div>
    <div class="product-overlay"></div>
  </div>
  <div class="product-info">
    <div class="product-footer">
      <div class="product-price">$38</div>
      <button class="product-btn">Shop Now</button>
    </div>
  </div>
</div>

<!-- Product 2 -->
<div class="product-card">
  <div class="product-img hat-bg-fitted">
    <div class="product-img-inner">
      <div style="font-family:'Bebas Neue',sans-serif;font-size:80px;line-height:1;text-shadow:0 0 30px rgba(139,0,0,0.7);">E<span style="color:#c0000a;font-size:56px;vertical-align:middle;">⚡</span>H</div>
    </div>
    <div class="product-overlay"></div>
  </div>
  <div class="product-info">
    <div class="product-footer">
      <div class="product-price">$45</div>
      <button class="product-btn">Shop Now</button>
    </div>
  </div>
</div>

<!-- Product 3 -->
<div class="product-card">
  <div class="product-img hat-bg-dad">
    <div class="product-img-inner">
      <div style="font-family:'Bebas Neue',sans-serif;font-size:80px;line-height:1;text-shadow:0 0 30px rgba(139,0,0,0.7);">E<span style="color:#c0000a;font-size:56px;vertical-align:middle;">⚡</span>H</div>
    </div>
    <div class="product-overlay"></div>
  </div>
  <div class="product-info">
    <div class="product-footer">
      <div class="product-price">$32</div>
      <button class="product-btn">Shop Now</button>
    </div>
  </div>
</div>
```

  </div>
</section>

<!-- ABOUT -->

<section id="about">
  <div class="about-grid">
    <div class="about-visual">
      <div class="about-logo-wrap">
        <div class="about-ring"></div>
        <div class="about-ring-2"></div>
        <div class="about-glow-bg"></div>
        <div style="position:relative;z-index:2;font-family:'Bebas Neue',sans-serif;font-size:100px;line-height:1;text-shadow:0 0 40px rgba(139,0,0,0.7);">E<span style="color:#c0000a;font-size:70px;vertical-align:middle;">⚡</span>H</div>
      </div>
    </div>
    <div class="about-text">
      <div class="section-label">/ 02 — Our Story</div>
      <div class="section-title">BUILT FOR<br>THE STREETS</div>
      <div class="divider"></div>
      <p class="about-body">Encargo Hats started with one mission — make headwear that hits different. Every cap is crafted with intention, inspired by street culture, and built to turn heads.</p>
      <p class="about-body">We don't do mass production. We do quality drops, custom pieces, and gear that means something. If you wear an EH cap, you already know.</p>
      <div class="about-stats">
        <div>
          <div class="stat-num">100<span style="font-size:32px;">%</span></div>
          <div class="stat-label">Quality Built</div>
        </div>
        <div>
          <div class="stat-num">∞</div>
          <div class="stat-label">Custom Options</div>
        </div>
        <div>
          <div class="stat-num">1<span style="font-size:32px;">ST</span></div>
          <div class="stat-label">In The Game</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->

<section id="contact">
  <div class="contact-grid">
    <div class="contact-info">
      <div class="section-label">/ 03 — Get In Touch</div>
      <div class="section-title">CUSTOM<br>ORDERS</div>
      <div class="divider"></div>
      <p class="contact-body">Want something built to your exact specs? Fill out the form and we'll get back to you with a quote. No idea too big, no detail too small.</p>
      <div class="contact-item">
        <div class="contact-icon">📍</div>
        <div>
          <div class="contact-item-label">Location</div>
          <div class="contact-item-val">Available Worldwide</div>
        </div>
      </div>
      <div class="contact-item">
        <div class="contact-icon">📸</div>
        <div>
          <div class="contact-item-label">Instagram</div>
          <div class="contact-item-val">@encargohats</div>
        </div>
      </div>
      <div class="contact-item">
        <div class="contact-icon">⚡</div>
        <div>
          <div class="contact-item-label">Turnaround</div>
          <div class="contact-item-val">2–4 Weeks for Custom Orders</div>
        </div>
      </div>
    </div>
    <div class="contact-form">
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">First Name</label>
          <input type="text" class="form-input" placeholder="Alex"/>
        </div>
        <div class="form-group">
          <label class="form-label">Last Name</label>
          <input type="text" class="form-input" placeholder="Rivera"/>
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Email</label>
        <input type="email" class="form-input" placeholder="you@email.com"/>
      </div>
      <div class="form-group">
        <label class="form-label">Hat Style</label>
        <select class="form-select form-input">
          <option value="" disabled selected>Select a style...</option>
          <option>Snapback</option>
          <option>Fitted Cap</option>
          <option>Dad Hat</option>
          <option>Trucker</option>
          <option>Beanie</option>
          <option>Other / Not Sure</option>
        </select>
      </div>
      <div class="form-group">
        <label class="form-label">Quantity</label>
        <select class="form-select form-input">
          <option value="" disabled selected>How many?</option>
          <option>1–5</option>
          <option>6–12</option>
          <option>13–24</option>
          <option>25+</option>
        </select>
      </div>
      <div class="form-group">
        <label class="form-label">Tell Us About Your Order</label>
        <textarea class="form-textarea" placeholder="Describe your design idea, colors, logos, text, or anything else..."></textarea>
      </div>
      <button class="form-submit" onclick="handleSubmit()">⚡ Send Order Request</button>
      <p class="form-note">We'll respond within 24–48 hours</p>
      <div class="success-msg" id="success-msg">✅ &nbsp; Message sent! We'll be in touch soon.</div>
    </div>
  </div>
</section>

<!-- FOOTER -->

<footer>
  <div class="footer-top">
    <div class="footer-brand">
      <div class="footer-logo">
        <div style="font-family:'Bebas Neue',sans-serif;font-size:24px;color:#f0ece8;">E<span style="color:#c0000a;">⚡</span>H</div>
        <span style="font-family:'Barlow Condensed',sans-serif;font-size:14px;letter-spacing:3px;color:rgba(240,236,232,0.5);">ENCARGO HATS</span>
      </div>
      <p class="footer-tagline">Premium headwear rooted in street culture. Every drop, every stitch, made to be worn and noticed.</p>
    </div>
    <div class="footer-links-group">
      <h4>Navigate</h4>
      <ul>
        <li><a href="#shop">Shop</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#contact">Contact</a></li>
        <li><a href="#contact">Custom Orders</a></li>
      </ul>
    </div>
    <div class="footer-links-group">
      <h4>Styles</h4>
      <ul>
        <li><a href="#shop">Snapbacks</a></li>
        <li><a href="#shop">Fitted Caps</a></li>
        <li><a href="#shop">Dad Hats</a></li>
        <li><a href="#contact">Custom</a></li>
      </ul>
    </div>
    <div class="footer-links-group">
      <h4>Info</h4>
      <ul>
        <li><a href="#">Sizing Guide</a></li>
        <li><a href="#">Shipping</a></li>
        <li><a href="#">Returns</a></li>
        <li><a href="#">FAQ</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <div class="footer-copy">© 2025 Encargo Hats. All rights reserved.</div>
    <div class="footer-socials">
      <a class="social-link" title="Instagram">📸</a>
      <a class="social-link" title="TikTok">🎵</a>
      <a class="social-link" title="Twitter/X">✖</a>
    </div>
  </div>
</footer>

<script>
  // Sticky nav
  const navbar = document.getElementById('navbar');
  window.addEventListener('scroll', () => {
    navbar.classList.toggle('scrolled', window.scrollY > 60);
  });

  // Form submit
  function handleSubmit() {
    const msg = document.getElementById('success-msg');
    msg.style.display = 'block';
    setTimeout(() => { msg.style.display = 'none'; }, 5000);
  }

  // Scroll reveal
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.style.opacity = '1';
        entry.target.style.transform = 'translateY(0)';
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.product-card, .about-stats .stat-num, .contact-item').forEach(el => {
    el.style.opacity = '0';
    el.style.transform = 'translateY(20px)';
    el.style.transition = 'opacity 0.6s ease, transform 0.6s ease';
    observer.observe(el);
  });
</script>

</body>
</html>
