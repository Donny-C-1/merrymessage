<main>
    <div class="hero">
        <h1>🎄 Welcome to MerryMessage 🎄</h1>
        <p>Create a heartfelt New Year message for your loved ones</p>
        <a class="btn" href="./create">Create Your Card</a>
        <div class="snowflakes" aria-hidden="true">
            <span>❅</span><span>❆</span><span>❅</span><span>❆</span><span>❅</span>
            <span>❆</span><span>❅</span><span>❆</span><span>❅</span><span>❆</span>
        </div>
    </div>
</main>

<style>
main {
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background: linear-gradient(to bottom, #1a2a6c, #b21f1f, #fdbb2d); /* festive gradient: night to gold */
    padding: 2rem;
    overflow: hidden;
    font-family: 'Quicksand', sans-serif;
}

.hero {
    text-align: center;
    background: rgba(255, 255, 255, 0.1);
    padding: 3rem 2rem;
    border-radius: 24px;
    backdrop-filter: blur(10px);
    box-shadow: 0 15px 35px rgba(0,0,0,0.3);
    position: relative;
    color: #fff;
}

h1 {
    font-size: 3rem;
    font-weight: 700;
    margin-bottom: 1rem;
    text-shadow: 2px 2px 8px rgba(0,0,0,0.3);
}

p {
    font-size: 1.25rem;
    font-weight: 500;
    margin-bottom: 2rem;
}

.btn {
    display: inline-block;
    padding: 1rem 2rem;
    font-size: 1.2rem;
    font-weight: 700;
    color: #fff;
    background: linear-gradient(45deg, #ff4b1f, #ff9068);
    border-radius: 12px;
    text-decoration: none;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
    box-shadow: 0 8px 20px rgba(0,0,0,0.3);
}

.btn:hover {
    transform: translateY(-3px);
    box-shadow: 0 12px 25px rgba(0,0,0,0.4);
}

/* Subtle snowflakes animation */
.snowflakes {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
}

.snowflakes span {
    position: absolute;
    color: #fff;
    font-size: 1rem;
    animation: fall 10s linear infinite;
    opacity: 0.8;
}

.snowflakes span:nth-child(1) { left: 10%; animation-delay: 0s; }
.snowflakes span:nth-child(2) { left: 20%; animation-delay: 2s; }
.snowflakes span:nth-child(3) { left: 30%; animation-delay: 4s; }
.snowflakes span:nth-child(4) { left: 40%; animation-delay: 1s; }
.snowflakes span:nth-child(5) { left: 50%; animation-delay: 3s; }
.snowflakes span:nth-child(6) { left: 60%; animation-delay: 5s; }
.snowflakes span:nth-child(7) { left: 70%; animation-delay: 2s; }
.snowflakes span:nth-child(8) { left: 80%; animation-delay: 4s; }
.snowflakes span:nth-child(9) { left: 90%; animation-delay: 6s; }
.snowflakes span:nth-child(10) { left: 100%; animation-delay: 8s; }

@keyframes fall {
    0% { transform: translateY(-10px); opacity: 0.8; }
    50% { opacity: 0.6; }
    100% { transform: translateY(100vh); opacity: 0; }
}

/* Responsive */
@media (max-width: 480px) {
    h1 { font-size: 2rem; }
    p { font-size: 1rem; }
    .btn { font-size: 1rem; padding: 0.75rem 1.5rem; }
}
</style>
