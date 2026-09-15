<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TradeCore | Realistic Trading UI</title>
  <!-- Font Awesome 6 (free) -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
    }

    body {
      background: #0b0e14;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      padding: 1.5rem;
    }

    /* main dashboard container */
    .dashboard {
      max-width: 1440px;
      width: 100%;
      background: #13171f;
      border-radius: 32px;
      box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.8), 0 0 0 1px rgba(255, 255, 255, 0.03);
      padding: 1.75rem 2rem 2rem 2rem;
      display: flex;
      flex-direction: column;
      gap: 1.75rem;
      border: 1px solid #2a2f3a;
    }

    /* header */
    .header {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .logo-area {
      display: flex;
      align-items: center;
      gap: 0.75rem;
    }

    .logo-icon {
      background: linear-gradient(145deg, #2962ff, #00b0ff);
      width: 40px;
      height: 40px;
      border-radius: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.4rem;
      color: white;
      box-shadow: 0 8px 18px -4px rgba(0, 98, 255, 0.3);
    }

    .logo-text {
      font-size: 1.5rem;
      font-weight: 700;
      letter-spacing: -0.02em;
      color: white;
    }

    .logo-text span {
      color: #4d7cff;
    }

    .header-actions {
      display: flex;
      align-items: center;
      gap: 1rem;
    }

    .search-bar {
      background: #1e232e;
      border-radius: 40px;
      padding: 0.6rem 1.2rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
      border: 1px solid #2b313d;
      transition: all 0.2s;
    }

    .search-bar i {
      color: #8b95a9;
      font-size: 0.9rem;
    }

    .search-bar input {
      background: transparent;
      border: none;
      outline: none;
      color: #eef2f6;
      font-size: 0.9rem;
      width: 180px;
    }

    .search-bar input::placeholder {
      color: #5c6478;
    }

    .user-profile {
      display: flex;
      align-items: center;
      gap: 0.8rem;
      background: #1e232e;
      padding: 0.4rem 0.8rem 0.4rem 0.4rem;
      border-radius: 40px;
      border: 1px solid #2b313d;
    }

    .avatar {
      width: 36px;
      height: 36px;
      background: linear-gradient(135deg, #2962ff, #a142f5);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 600;
      color: white;
      font-size: 0.9rem;
    }

    .user-info {
      display: flex;
      flex-direction: column;
    }

    .user-info .name {
      font-size: 0.9rem;
      font-weight: 600;
      color: #eef2f6;
    }

    .user-info .role {
      font-size: 0.7rem;
      color: #8b95a9;
    }

    /* main grid */
    .main-grid {
      display: grid;
      grid-template-columns: 1fr 1.8fr 1fr;
      gap: 1.5rem;
    }

    /* left panel */
    .left-panel {
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
    }

    .balance-card {
      background: linear-gradient(145deg, #0f1219, #161b26);
      border-radius: 24px;
      padding: 1.5rem;
      border: 1px solid #2a2f3a;
      box-shadow: 0 10px 20px -5px rgba(0, 0, 0, 0.5);
    }

    .balance-label {
      display: flex;
      justify-content: space-between;
      color: #8b95a9;
      font-size: 0.85rem;
      font-weight: 500;
      letter-spacing: 0.3px;
      text-transform: uppercase;
      margin-bottom: 0.5rem;
    }

    .balance-amount {
      font-size: 2.2rem;
      font-weight: 700;
      color: white;
      letter-spacing: -0.02em;
      margin-bottom: 0.2rem;
    }

    .balance-amount small {
      font-size: 1rem;
      font-weight: 400;
      color: #8b95a9;
      margin-left: 0.3rem;
    }

    .balance-change {
      display: flex;
      align-items: center;
      gap: 0.4rem;
      font-size: 0.85rem;
      color: #26a69a;
      background: rgba(38, 166, 154, 0.1);
      padding: 0.3rem 0.7rem;
      border-radius: 40px;
      width: fit-content;
      margin-top: 0.5rem;
      font-weight: 500;
    }

    .balance-change i {
      font-size: 0.7rem;
    }

    .watchlist {
      background: #0f1219;
      border-radius: 24px;
      padding: 1.5rem;
      border: 1px solid #2a2f3a;
      flex: 1;
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }

    .section-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      color: #eef2f6;
      font-weight: 600;
      font-size: 1rem;
      letter-spacing: -0.01em;
    }

    .section-header i {
      color: #5c6478;
      font-size: 0.9rem;
      cursor: pointer;
      transition: color 0.2s;
    }

    .section-header i:hover {
      color: #b0b8c5;
    }

    .watchlist-items {
      display: flex;
      flex-direction: column;
      gap: 0.9rem;
    }

    .watch-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0.3rem 0;
      border-bottom: 1px solid #1e232e;
      cursor: default;
    }

    .watch-item:last-child {
      border-bottom: none;
    }

    .ticker-info {
      display: flex;
      flex-direction: column;
    }

    .ticker-symbol {
      font-weight: 600;
      color: #eef2f6;
      font-size: 0.95rem;
    }

    .ticker-name {
      font-size: 0.7rem;
      color: #6b7588;
    }

    .ticker-price {
      text-align: right;
    }

    .price-value {
      font-weight: 600;
      color: #eef2f6;
      font-size: 0.95rem;
    }

    .price-change {
      font-size: 0.7rem;
      font-weight: 500;
    }

    .positive {
      color: #26a69a;
    }

    .negative {
      color: #ef5350;
    }

    /* center panel */
    .center-panel {
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
    }

    .chart-container {
      background: #0f1219;
      border-radius: 24px;
      padding: 1.5rem;
      border: 1px solid #2a2f3a;
    }

    .chart-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 1.2rem;
    }

    .pair-selector {
      display: flex;
      align-items: center;
      gap: 0.75rem;
    }

    .pair-icon {
      background: #1e232e;
      width: 40px;
      height: 40px;
      border-radius: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #4d7cff;
      font-weight: 700;
      font-size: 1.1rem;
      border: 1px solid #2b313d;
    }

    .pair-details h3 {
      color: white;
      font-size: 1.1rem;
      font-weight: 700;
      letter-spacing: -0.01em;
    }

    .pair-details span {
      color: #8b95a9;
      font-size: 0.7rem;
      font-weight: 500;
    }

    .price-big {
      text-align: right;
    }

    .price-big .current {
      font-size: 1.8rem;
      font-weight: 700;
      color: white;
      letter-spacing: -0.02em;
    }

    .price-big .change {
      font-size: 0.85rem;
      font-weight: 500;
      color: #26a69a;
    }

    /* canvas chart placeholder with realistic grid */
    .chart-area {
      position: relative;
      height: 200px;
      width: 100%;
      background: #0b0e14;
      border-radius: 16px;
      overflow: hidden;
      border: 1px solid #1e232e;
    }

    .chart-grid {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-image: 
        linear-gradient(to right, #1e232e 1px, transparent 1px),
        linear-gradient(to bottom, #1e232e 1px, transparent 1px);
      background-size: 40px 40px;
      opacity: 0.5;
    }

    .chart-line {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 100%;
    }

    /* simple svg chart */
    .chart-svg {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 100%;
    }

    /* order book / trades */
    .order-book {
      background: #0f1219;
      border-radius: 24px;
      padding: 1.5rem;
      border: 1px solid #2a2f3a;
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }

    .book-tabs {
      display: flex;
      gap: 1.5rem;
      border-bottom: 1px solid #1e232e;
      padding-bottom: 0.5rem;
    }

    .book-tab {
      color: #6b7588;
      font-weight: 500;
      font-size: 0.9rem;
      cursor: pointer;
      padding-bottom: 0.5rem;
      transition: all 0.2s;
    }

    .book-tab.active {
      color: white;
      border-bottom: 2px solid #4d7cff;
      margin-bottom: -1px;
    }

    .orders-list {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }

    .order-row {
      display: flex;
      justify-content: space-between;
      font-size: 0.85rem;
      padding: 0.3rem 0;
    }

    .order-price {
      font-weight: 500;
    }

    .order-price.bid {
      color: #26a69a;
    }

    .order-price.ask {
      color: #ef5350;
    }

    .order-amount {
      color: #b0b8c5;
      font-weight: 400;
    }

    .order-total {
      color: #6b7588;
      font-weight: 400;
    }

    /* right panel */
    .right-panel {
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
    }

    .trade-form {
      background: #0f1219;
      border-radius: 24px;
      padding: 1.5rem;
      border: 1px solid #2a2f3a;
    }

    .trade-type {
      display: flex;
      background: #1a1f2a;
      border-radius: 40px;
      padding: 0.25rem;
      margin-bottom: 1.5rem;
    }

    .trade-type button {
      flex: 1;
      background: transparent;
      border: none;
      padding: 0.6rem 0;
      border-radius: 40px;
      font-weight: 600;
      font-size: 0.9rem;
      color: #8b95a9;
      cursor: pointer;
      transition: all 0.2s;
    }

    .trade-type button.active {
      background: #2962ff;
      color: white;
      box-shadow: 0 4px 12px rgba(41, 98, 255, 0.3);
    }

    .input-group {
      margin-bottom: 1rem;
    }

    .input-group label {
      display: block;
      color: #8b95a9;
      font-size: 0.75rem;
      font-weight: 500;
      margin-bottom: 0.4rem;
      text-transform: uppercase;
      letter-spacing: 0.3px;
    }

    .input-wrapper {
      background: #1a1f2a;
      border-radius: 12px;
      padding: 0.75rem 1rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border: 1px solid #2b313d;
      transition: border 0.2s;
    }

    .input-wrapper:focus-within {
      border-color: #2962ff;
    }

    .input-wrapper input {
      background: transparent;
      border: none;
      outline: none;
      color: white;
      font-size: 1rem;
      font-weight: 500;
      width: 100%;
    }

    .input-wrapper span {
      color: #8b95a9;
      font-size: 0.85rem;
      font-weight: 500;
    }

    .percent-buttons {
      display: flex;
      gap: 0.5rem;
      margin: 1rem 0 1.2rem;
    }

    .percent-buttons button {
      background: #1a1f2a;
      border: 1px solid #2b313d;
      color: #b0b8c5;
      font-size: 0.75rem;
      font-weight: 500;
      padding: 0.4rem 0;
      border-radius: 30px;
      flex: 1;
      cursor: pointer;
      transition: all 0.15s;
    }

    .percent-buttons button:hover {
      background: #252b37;
      border-color: #3e4553;
    }

    .action-button {
      width: 100%;
      background: #26a69a;
      border: none;
      padding: 1rem;
      border-radius: 14px;
      font-weight: 700;
      font-size: 1rem;
      color: white;
      cursor: pointer;
      transition: all 0.2s;
      margin-top: 0.5rem;
      box-shadow: 0 8px 18px -4px rgba(38, 166, 154, 0.3);
    }

    .action-button.sell {
      background: #ef5350;
      box-shadow: 0 8px 18px -4px rgba(239, 83, 80, 0.3);
    }

    .action-button:hover {
      filter: brightness(1.1);
      transform: translateY(-1px);
    }

    .recent-trades {
      background: #0f1219;
      border-radius: 24px;
      padding: 1.5rem;
      border: 1px solid #2a2f3a;
      flex: 1;
    }

    .trade-item {
      display: flex;
      justify-content: space-between;
      padding: 0.5rem 0;
      border-bottom: 1px solid #1a1f2a;
      font-size: 0.85rem;
    }

    .trade-item:last-child {
      border-bottom: none;
    }

    .trade-pair {
      font-weight: 600;
      color: #eef2f6;
    }

    .trade-side {
      font-size: 0.7rem;
      padding: 0.2rem 0.5rem;
      border-radius: 20px;
      font-weight: 600;
      margin-left: 0.5rem;
    }

    .trade-side.buy {
      background: rgba(38, 166, 154, 0.15);
      color: #26a69a;
    }

    .trade-side.sell {
      background: rgba(239, 83, 80, 0.15);
      color: #ef5350;
    }

    .trade-amount {
      color: #b0b8c5;
    }

    .trade-time {
      color: #6b7588;
      font-size: 0.75rem;
    }

    /* responsiveness */
    @media (max-width: 1200px) {
      .main-grid {
        grid-template-columns: 1fr 1fr;
      }
      .right-panel {
        grid-column: span 2;
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 1.5rem;
      }
    }

    @media (max-width: 800px) {
      .dashboard {
        padding: 1.25rem;
      }
      .main-grid {
        grid-template-columns: 1fr;
      }
      .right-panel {
        grid-column: span 1;
        grid-template-columns: 1fr;
      }
      .header {
        flex-direction: column;
        align-items: flex-start;
        gap: 1rem;
      }
      .header-actions {
        width: 100%;
        justify-content: space-between;
      }
      .search-bar input {
        width: 120px;
      }
    }
  </style>
</head>
<body>
  <div class="dashboard">
    <!-- header -->
    <div class="header">
      <div class="logo-area">
        <div class="logo-icon">
          <i class="fas fa-chart-line"></i>
        </div>
        <div class="logo-text">Trade<span>Core</span></div>
      </div>
      <div class="header-actions">
        <div class="search-bar">
          <i class="fas fa-search"></i>
          <input type="text" placeholder="Search markets...">
        </div>
        <div class="user-profile">
          <div class="avatar">JD</div>
          <div class="user-info">
            <span class="name">James Doyle</span>
            <span class="role">Pro Trader</span>
          </div>
        </div>
      </div>
    </div>

    <!-- main content grid -->
    <div class="main-grid">
      <!-- left panel -->
      <div class="left-panel">
        <div class="balance-card">
          <div class="balance-label">
            <span>Portfolio Value</span>
            <i class="fas fa-chevron-right" style="color: #5c6478; font-size: 0.7rem;"></i>
          </div>
          <div class="balance-amount">$48,320<small>USD</small></div>
          <div class="balance-change">
            <i class="fas fa-arrow-up"></i> +$1,240 (2.6%) today
          </div>
        </div>

        <div class="watchlist">
          <div class="section-header">
            <span>Watchlist</span>
            <i class="fas fa-ellipsis-h"></i>
          </div>
          <div class="watchlist-items">
            <div class="watch-item">
              <div class="ticker-info">
                <span class="ticker-symbol">BTC/USD</span>
                <span class="ticker-name">Bitcoin</span>
              </div>
              <div class="ticker-price">
                <div class="price-value">$63,420</div>
                <div class="price-change positive">+2.4%</div>
              </div>
            </div>
            <div class="watch-item">
              <div class="ticker-info">
                <span class="ticker-symbol">ETH/USD</span>
                <span class="ticker-name">Ethereum</span>
              </div>
              <div class="ticker-price">
                <div class="price-value">$3,125</div>
                <div class="price-change positive">+1.8%</div>
              </div>
            </div>
            <div class="watch-item">
              <div class="ticker-info">
                <span class="ticker-symbol">AAPL</span>
                <span class="ticker-name">Apple Inc.</span>
              </div>
              <div class="ticker-price">
                <div class="price-value">$189.45</div>
                <div class="price-change negative">-0.7%</div>
              </div>
            </div>
            <div class="watch-item">
              <div class="ticker-info">
                <span class="ticker-symbol">TSLA</span>
                <span class="ticker-name">Tesla</span>
              </div>
              <div class="ticker-price">
                <div class="price-value">$245.30</div>
                <div class="price-change positive">+3.2%</div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- center panel -->
      <div class="center-panel">
        <div class="chart-container">
          <div class="chart-header">
            <div class="pair-selector">
              <div class="pair-icon">₿</div>
              <div class="pair-details">
                <h3>BTC / USD</h3>
                <span>Bitcoin · Cryptocurrency</span>
              </div>
            </div>
            <div class="price-big">
              <div class="current">$63,420.50</div>
              <div class="change">+$1,510.20 (2.44%)</div>
            </div>
          </div>
          <div class="chart-area">
            <div class="chart-grid"></div>
            <!-- realistic SVG line chart -->
            <svg class="chart-svg" viewBox="0 0 500 200" preserveAspectRatio="none">
              <!-- gradient area fill -->
              <defs>
                <linearGradient id="chartGrad" x1="0" y1="0" x2="0" y2="1">
                  <stop offset="0%" stop-color="#2962ff" stop-opacity="0.3"/>
                  <stop offset="100%" stop-color="#2962ff" stop-opacity="0"/>
                </linearGradient>
              </defs>
              <!-- area fill -->
              <path d="M0 150 L30 140 L60 130 L90 135 L120 110 L150 95 L180 100 L210 75 L240 60 L270 50 L300 45 L330 30 L360 40 L390 25 L420 15 L450 30 L480 20 L500 10 L500 200 L0 200 Z" 
                    fill="url(#chartGrad)" stroke="none" />
              <!-- line -->
              <path d="M0 150 L30 140 L60 130 L90 135 L120 110 L150 95 L180 100 L210 75 L240 60 L270 50 L300 45 L330 30 L360 40 L390 25 L420 15 L450 30 L480 20 L500 10" 
                    fill="none" stroke="#4d7cff" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" />
              <!-- dots -->
              <circle cx="500" cy="10" r="4" fill="#4d7cff" stroke="#0b0e14" stroke-width="2" />
            </svg>
          </div>
        </div>

        <!-- order book / trades -->
        <div class="order-book">
          <div class="book-tabs">
            <span class="book-tab active">Order Book</span>
            <span class="book-tab">Market Trades</span>
          </div>
          <div class="orders-list">
            <div class="order-row">
              <span class="order-price ask">63,425.50</span>
              <span class="order-amount">0.45 BTC</span>
              <span class="order-total">$28,541</span>
            </div>
            <div class="order-row">
              <span class="order-price ask">63,424.00</span>
              <span class="order-amount">1.20 BTC</span>
              <span class="order-total">$76,108</span>
            </div>
            <div class="order-row">
              <span class="order-price ask">63,422.80</span>
              <span class="order-amount">0.80 BTC</span>
           