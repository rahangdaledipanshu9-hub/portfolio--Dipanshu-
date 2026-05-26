/* ============================================================
   Dipanshu Rahangdale — Portfolio Script
   Dark Industrial Luxury Edition
   ============================================================ */

(function () {
    'use strict';

    /* ── Helpers ──────────────────────────────────────────── */
    function qs(sel)  { return document.querySelector(sel); }
    function qsa(sel) { return document.querySelectorAll(sel); }

    let rafPending = false;
    const scrollCBs = [];
    function onScroll(fn) { scrollCBs.push(fn); }
    window.addEventListener('scroll', function () {
        if (rafPending) return;
        rafPending = true;
        requestAnimationFrame(function () {
            rafPending = false;
            const y = window.pageYOffset;
            scrollCBs.forEach(function (fn) { fn(y); });
        });
    }, { passive: true });

    /* ── Preloader ────────────────────────────────────────── */
    const preloader = qs('#preloader');
    window.addEventListener('load', function () {
        setTimeout(function () {
            preloader.classList.add('done');
            setTimeout(function () { preloader.remove(); }, 700);
        }, 800);
    });

    /* ── Custom Cursor ────────────────────────────────────── */
    const dot  = qs('#cursorDot');
    const ring = qs('#cursorRing');
    if (dot && ring && window.matchMedia('(pointer:fine)').matches) {
        let mx = 0, my = 0, rx = 0, ry = 0;
        document.addEventListener('mousemove', function (e) {
            mx = e.clientX; my = e.clientY;
            dot.style.transform  = 'translate(' + (mx - 3)  + 'px,' + (my - 3)  + 'px)';
        });
        (function animRing() {
            rx += (mx - rx) * 0.12;
            ry += (my - ry) * 0.12;
            ring.style.transform = 'translate(' + (rx - 18) + 'px,' + (ry - 18) + 'px)';
            requestAnimationFrame(animRing);
        })();
        /* Hover effect */
        qsa('a,button,.proj-card,.acard,.cert-item,.tl-card').forEach(function (el) {
            el.addEventListener('mouseenter', function () {
                ring.style.width  = '60px';
                ring.style.height = '60px';
                ring.style.borderColor = 'rgba(201,168,76,0.9)';
                dot.style.opacity = '0';
            });
            el.addEventListener('mouseleave', function () {
                ring.style.width  = '36px';
                ring.style.height = '36px';
                ring.style.borderColor = 'rgba(201,168,76,0.5)';
                dot.style.opacity = '1';
            });
        });
    } else {
        if (dot)  dot.remove();
        if (ring) ring.remove();
        document.body.style.cursor = 'auto';
    }

    /* ── Hero Canvas — Molecular Network ─────────────────── */
    const canvas = qs('#heroCanvas');
    if (canvas) {
        const ctx = canvas.getContext('2d');
        let W, H, nodes = [];

        function resize() {
            W = canvas.width  = canvas.offsetWidth;
            H = canvas.height = canvas.offsetHeight;
        }
        resize();
        window.addEventListener('resize', resize);

        const NODE_COUNT = 55;
        const MAX_DIST   = 160;

        for (let i = 0; i < NODE_COUNT; i++) {
            nodes.push({
                x:  Math.random() * (typeof W !== 'undefined' ? W : 1200),
                y:  Math.random() * (typeof H !== 'undefined' ? H : 700),
                vx: (Math.random() - 0.5) * 0.4,
                vy: (Math.random() - 0.5) * 0.4,
                r:  Math.random() * 2 + 1
            });
        }

        function drawFrame() {
            ctx.clearRect(0, 0, W, H);
            // move
            nodes.forEach(function (n) {
                n.x += n.vx; n.y += n.vy;
                if (n.x < 0 || n.x > W) n.vx *= -1;
                if (n.y < 0 || n.y > H) n.vy *= -1;
            });
            // edges
            for (let i = 0; i < nodes.length; i++) {
                for (let j = i + 1; j < nodes.length; j++) {
                    const dx = nodes[i].x - nodes[j].x;
                    const dy = nodes[i].y - nodes[j].y;
                    const d  = Math.sqrt(dx * dx + dy * dy);
                    if (d < MAX_DIST) {
                        const alpha = (1 - d / MAX_DIST) * 0.22;
                        ctx.strokeStyle = 'rgba(201,168,76,' + alpha + ')';
                        ctx.lineWidth   = 0.8;
                        ctx.beginPath();
                        ctx.moveTo(nodes[i].x, nodes[i].y);
                        ctx.lineTo(nodes[j].x, nodes[j].y);
                        ctx.stroke();
                    }
                }
            }
            // nodes
            nodes.forEach(function (n) {
                ctx.beginPath();
                ctx.arc(n.x, n.y, n.r, 0, Math.PI * 2);
                ctx.fillStyle = 'rgba(201,168,76,0.55)';
                ctx.fill();
            });
            requestAnimationFrame(drawFrame);
        }
        drawFrame();
    }

    /* ── Role Cycling Text ────────────────────────────────── */
    const words = qsa('.role-word');
    if (words.length) {
        let cur = 0;
        setInterval(function () {
            words[cur].classList.remove('active');
            words[cur].classList.add('out');
            const prev = cur;
            cur = (cur + 1) % words.length;
            words[cur].classList.add('active');
            setTimeout(function () { words[prev].classList.remove('out'); }, 550);
        }, 2800);
    }

    /* ── Counter Animation ────────────────────────────────── */
    function animateCounter(el) {
        const target = parseInt(el.getAttribute('data-target'), 10);
        let current  = 0;
        const step   = Math.ceil(target / 40);
        const timer  = setInterval(function () {
            current += step;
            if (current >= target) { current = target; clearInterval(timer); }
            el.textContent = current + '+';
        }, 40);
    }
    const counterObs = new IntersectionObserver(function (entries) {
        entries.forEach(function (entry) {
            if (entry.isIntersecting) {
                animateCounter(entry.target);
                counterObs.unobserve(entry.target);
            }
        });
    }, { threshold: 0.5 });
    qsa('.hstat-num[data-target]').forEach(function (el) { counterObs.observe(el); });

    /* ── Navbar ───────────────────────────────────────────── */
    const navbar    = qs('#navbar');
    const hamburger = qs('#hamburger');
    const navMenu   = qs('#navMenu');
    const navLinks  = qsa('.nav-link');
    const sections  = qsa('section[id]');

    hamburger && hamburger.addEventListener('click', function () {
        const open = navMenu.classList.toggle('active');
        hamburger.classList.toggle('active', open);
        document.body.style.overflow = open ? 'hidden' : '';
    });
    navLinks.forEach(function (l) {
        l.addEventListener('click', function () {
            navMenu.classList.remove('active');
            hamburger && hamburger.classList.remove('active');
            document.body.style.overflow = '';
        });
    });
    document.addEventListener('keydown', function (e) {
        if (e.key === 'Escape' && navMenu.classList.contains('active')) {
            navMenu.classList.remove('active');
            hamburger && hamburger.classList.remove('active');
            document.body.style.overflow = '';
        }
    });

    onScroll(function (y) {
        navbar && navbar.classList.toggle('scrolled', y > 80);
    });

    /* Active nav link */
    onScroll(function (y) {
        const pos = y + 160;
        sections.forEach(function (sec) {
            if (pos >= sec.offsetTop && pos < sec.offsetTop + sec.offsetHeight) {
                const id = sec.getAttribute('id');
                navLinks.forEach(function (l) {
                    l.classList.toggle('active', l.getAttribute('href') === '#' + id);
                });
            }
        });
    });

    /* Smooth scroll */
    qsa('a[href^="#"]').forEach(function (a) {
        a.addEventListener('click', function (e) {
            const href = this.getAttribute('href');
            if (href === '#') return;
            const target = qs(href);
            if (!target) return;
            e.preventDefault();
            window.scrollTo({ top: target.offsetTop - 90, behavior: 'smooth' });
        });
    });

    /* ── Scroll-to-Top ────────────────────────────────────── */
    const scrollTopBtn = qs('#scrollToTop');
    if (scrollTopBtn) {
        onScroll(function (y) {
            scrollTopBtn.classList.toggle('visible', y > 500);
        });
        scrollTopBtn.addEventListener('click', function () {
            window.scrollTo({ top: 0, behavior: 'smooth' });
        });
    }

    /* ── Reveal on Scroll ─────────────────────────────────── */
    document.body.classList.add('js-ready');
    const revealItems = qsa('.reveal-item');

    const safetyTimer = setTimeout(function () {
        revealItems.forEach(function (el) { el.classList.add('revealed'); });
    }, 2500);

    if ('IntersectionObserver' in window) {
        const revObs = new IntersectionObserver(function (entries) {
            entries.forEach(function (entry) {
                if (entry.isIntersecting) {
                    entry.target.classList.add('revealed');
                    revObs.unobserve(entry.target);
                }
            });
        }, { threshold: 0.07, rootMargin: '0px 0px -50px 0px' });

        revealItems.forEach(function (el) { revObs.observe(el); });

        let done = 0;
        revealItems.forEach(function (el) {
            el.addEventListener('transitionend', function () {
                if (++done >= revealItems.length) clearTimeout(safetyTimer);
            }, { once: true });
        });
    } else {
        clearTimeout(safetyTimer);
        revealItems.forEach(function (el) { el.classList.add('revealed'); });
    }

    /* ── Skill Bar Animation ──────────────────────────────── */
    const skillObs = new IntersectionObserver(function (entries) {
        entries.forEach(function (entry) {
            if (!entry.isIntersecting) return;
            entry.target.querySelectorAll('.skill-progress').forEach(function (bar) {
                const w = bar.getAttribute('data-width') || '0';
                setTimeout(function () { bar.style.width = w + '%'; }, 250);
            });
            skillObs.unobserve(entry.target);
        });
    }, { threshold: 0.25 });

    qsa('.skill-list').forEach(function (list) { skillObs.observe(list); });

    /* ── Staggered Reveal for Cards ───────────────────────── */
    qsa('.about-cards, .certs-grid, .projects-grid').forEach(function (grid) {
        const children = grid.querySelectorAll('.acard, .cert-item, .proj-card');
        children.forEach(function (child, i) {
            child.style.transitionDelay = (i * 0.07) + 's';
        });
    });

    /* ── Tilt effect on project cards ────────────────────── */
    qsa('.proj-card').forEach(function (card) {
        card.addEventListener('mousemove', function (e) {
            const rect = card.getBoundingClientRect();
            const x = (e.clientX - rect.left) / rect.width  - 0.5;
            const y = (e.clientY - rect.top)  / rect.height - 0.5;
            card.style.transform = 'translateY(-6px) rotateX(' + (-y * 5) + 'deg) rotateY(' + (x * 5) + 'deg)';
        });
        card.addEventListener('mouseleave', function () {
            card.style.transform = '';
        });
    });

    /* ── Contact Form ─────────────────────────────────────── */
    const contactForm = qs('#contactForm');
    if (contactForm) {
        contactForm.addEventListener('submit', function (e) {
            e.preventDefault();
            const name    = qs('#name').value.trim();
            const email   = qs('#email').value.trim();
            const subject = qs('#subject').value.trim();
            const message = qs('#message').value.trim();
            if (!name || !email || !subject || !message) {
                showToast('Please fill in all fields.', 'error');
                return;
            }
            const body = 'Name: ' + name + '\nEmail: ' + email + '\n\nMessage:\n' + message;
            window.location.href = 'mailto:rahangdaledipanshu9@gmail.com'
                + '?subject=' + encodeURIComponent(subject)
                + '&body='    + encodeURIComponent(body);
            showToast('Opening your email client…', 'success');
            contactForm.reset();
        });
    }

    /* ── Toast ────────────────────────────────────────────── */
    function showToast(msg, type) {
        const existing = qs('.toast');
        if (existing) existing.remove();
        const t = document.createElement('div');
        t.className = 'toast';
        const isErr = type === 'error';
        if (isErr) t.style.borderLeftColor = 'var(--red)';
        t.innerHTML =
            '<i class="fas ' + (isErr ? 'fa-exclamation-circle' : 'fa-check-circle') + '" '
            + 'style="color:' + (isErr ? 'var(--red)' : 'var(--green)') + '"></i>'
            + '<span>' + msg + '</span>';
        document.body.appendChild(t);
        setTimeout(function () {
            t.classList.add('removing');
            setTimeout(function () { t.remove(); }, 400);
        }, 3400);
    }

    /* ── Glitch effect on hero name (subtle, periodic) ───── */
    const hnLast = qs('.hn-last');
    if (hnLast) {
        setInterval(function () {
            hnLast.style.textShadow =
                '2px 0 rgba(201,168,76,0.7), -2px 0 rgba(74,158,255,0.5)';
            setTimeout(function () {
                hnLast.style.textShadow = '';
            }, 120);
        }, 5000);
    }

    /* ── Parallax on photo glow ───────────────────────────── */
    const photoGlow = qs('.photo-glow');
    if (photoGlow && window.matchMedia('(pointer:fine)').matches) {
        document.addEventListener('mousemove', function (e) {
            const x = (e.clientX / window.innerWidth  - 0.5) * 20;
            const y = (e.clientY / window.innerHeight - 0.5) * 20;
            photoGlow.style.transform = 'translate(' + x + 'px,' + y + 'px)';
        });
    }

    /* ── Console branding ─────────────────────────────────── */
    console.log('%c⬡  DIPANSHU RAHANGDALE', 'color:#c9a84c;font-size:20px;font-weight:900;letter-spacing:2px;');
    console.log('%cChemical Engineer · Researcher · SIH 2025 Grand Winner', 'color:#525a68;font-size:12px;');
    console.log('%crahangdaledipanshu9@gmail.com', 'color:#4a9eff;font-size:11px;');

})();
