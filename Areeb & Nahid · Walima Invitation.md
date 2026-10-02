<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Wedding Invitation</title>
  
  <!-- گوگل فونٹس -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600&family=Great+Vibes&family=Montserrat:wght@300;400&display=swap" rel="stylesheet">

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background-color: #2b2820;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      font-family: 'Cinzel', serif;
      overflow: hidden;
    }

    /* اینولپ کنٹینر */
    .envelope-wrapper {
      position: relative;
      width: 340px;
      height: 520px;
      cursor: pointer;
      perspective: 1200px;
    }

    /* لفافہ بیس */
    .envelope {
      position: relative;
      width: 100%;
      height: 100%;
      background: #5b5340; /* Olive/Brown Color */
      border-radius: 8px;
      box-shadow: 0 25px 45px rgba(0, 0, 0, 0.45);
      overflow: visible;
    }

    /* ہلکی پیپر ٹیکسچر لک */
    .envelope::before {
      content: '';
      position: absolute;
      inset: 0;
      background: radial-gradient(circle at 50% 50%, rgba(255, 255, 255, 0.05), transparent 70%);
      pointer-events: none;
      border-radius: 8px;
    }

    /* اوپر کی تحریر (Names & Subtext) */
    .front-text {
      position: absolute;
      top: 30%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 90%;
      text-align: center;
      z-index: 10;
      pointer-events: none;
      transition: opacity 0.5s ease;
    }

    .front-text .names {
      font-family: 'Great Vibes', cursive;
      font-size: 38px;
      color: #eae5d9;
      font-weight: normal;
      text-shadow: 0 1px 3px rgba(0, 0, 0, 0.3);
      white-space: nowrap;
    }

    .front-text .subtext {
      font-family: 'Cinzel', serif;
      font-size: 11px;
      letter-spacing: 3px;
      color: #d1c8b4;
      margin-top: 6px;
      text-transform: uppercase;
      opacity: 0.9;
    }

    /* اوپری تکونہ فلیپ (Flap) */
    .flap {
      position: absolute;
      top: 0;
      left: 0;
      width: 0;
      height: 0;
      border-left: 170px solid transparent;
      border-right: 170px solid transparent;
      border-top: 260px solid #524b3a;
      transform-origin: top;
      transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1), z-index 0.2s 0.3s;
      z-index: 5;
      filter: drop-shadow(0 6px 10px rgba(0, 0, 0, 0.25));
    }

    /* اندرونی شادی کا کارڈ */
    .letter {
      position: absolute;
      top: 15px;
      left: 15px;
      width: 310px;
      height: 480px;
      background: #fbf9f5;
      border-radius: 6px;
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.15);
      z-index: 3;
      padding: 30px 20px;
      text-align: center;
      transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1) 0.5s, z-index 0.1s 0.5s;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      border: 1px solid #dcd4c3;
    }

    .letter h3 {
      font-family: 'Cinzel', serif;
      font-size: 14px;
      letter-spacing: 4px;
      color: #837861;
      margin-bottom: 12px;
    }

    .letter h2 {
      font-family: 'Great Vibes', cursive;
      font-size: 34px;
      color: #3f392c;
      margin-bottom: 15px;
      font-weight: normal;
    }

    .letter p {
      font-family: 'Montserrat', sans-serif;
      font-size: 11px;
      line-height: 1.7;
      color: #615a4c;
      letter-spacing: 1px;
    }

    .letter .date {
      margin-top: 15px;
      font-weight: 600;
      color: #4a4334;
      font-size: 12px;
      letter-spacing: 2px;
    }

    /* ویکس سیل (Wax Seal) */
    .wax-seal {
      position: absolute;
      top: 52%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 65px;
      height: 65px;
      background: radial-gradient(circle, #e3dbc9 20%, #c4b9a1 90%);
      border-radius: 50%;
      box-shadow: 0 4px 10px rgba(0,0,0,0.35),
                  inset 0 2px 4px rgba(255,255,255,0.4),
                  inset 0 -3px 5px rgba(0,0,0,0.2);
      z-index: 6;
      display: flex;
      justify-content: center;
      align-items: center;
      transition: transform 0.6s ease, opacity 0.4s ease;
    }

    .wax-seal::after {
      content: '';
      position: absolute;
      inset: -4px;
      border-radius: 46% 54% 48% 52% / 53% 47% 53% 47%;
      border: 3px solid rgba(186, 175, 151, 0.6);
      pointer-events: none;
    }

    .wax-seal svg {
      width: 28px;
      height: 28px;
      fill: #82755e;
      opacity: 0.85;
      filter: drop-shadow(0 1px 1px rgba(255,255,255,0.4));
    }

    /* نیچے کا ٹیکسٹ */
    .bottom-hint {
      position: absolute;
      bottom: 25px;
      left: 0;
      width: 100%;
      text-align: center;
      font-size: 9px;
      letter-spacing: 3px;
      color: #9c9179;
      text-transform: uppercase;
      opacity: 0.8;
      pointer-events: none;
      transition: opacity 0.4s ease;
      z-index: 10;
    }

    /* اوپن اینیمیشن (Click State) */
    .envelope-wrapper.open .flap {
      transform: rotateX(180deg);
      z-index: 1;
    }

    .envelope-wrapper.open .wax-seal {
      opacity: 0;
      transform: translate(-50%, -70%) scale(0.6);
      pointer-events: none;
    }

    .envelope-wrapper.open .bottom-hint {
      opacity: 0;
    }

    .envelope-wrapper.open .letter {
      transform: translateY(-160px);
      z-index: 7;
      box-shadow: 0 15px 30px rgba(0,0,0,0.35);
    }
  </style>
</head>
<body>

  <div class="envelope-wrapper" id="envelopeWrapper">
    <div class="envelope">
      
      <div class="front-text">
        <h1 class="names">Camilla & Matthew</h1>
        <div class="subtext">Are Getting Married!</div>
      </div>

      <div class="flap"></div>

      <div class="wax-seal">
        <svg viewBox="0 0 24 24">
          <path d="M12 2C10.5 4.5 9 8 9 11c0 3 2 5.5 3 6.5 1-1 3-3.5 3-6.5 0-3-1.5-6.5-3-9zm-1 15.5c-2-1-4-3-4.5-5.5 2 .5 4 2 4.5 5.5zm2 0c.5-3.5 2.5-5 4.5-5.5-.5 2.5-2.5 4.5-4.5 5.5z"/>
          <path d="M12 18v4" stroke="#82755e" stroke-width="1.5" stroke-linecap="round"/>
        </svg>
      </div>

      <div class="letter">
        <h3>Save the Date</h3>
        <h2>Camilla & Matthew</h2>
        <p>Request the pleasure of your company at their wedding celebration</p>
        <div class="date">SATURDAY, OCTOBER 24</div>
        <p style="margin-top: 10px; font-size: 10px; color: #8c826e;">AT FIVE IN THE EVENING</p>
      </div>

      <div class="bottom-hint">Click Envelope To Open</div>
    </div>
  </div>

  <script>
    const envelopeWrapper = document.getElementById('envelopeWrapper');
    envelopeWrapper.addEventListener('click', () => {
      envelopeWrapper.classList.toggle('open');
    });
  </script>

</body>
</html>