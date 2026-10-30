<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>原子量・分子量・式量 マスターゲーム</title>

  <style>
    :root {
      --blue: #1763b1;
      --blue-dark: #0d4b89;
      --text: #17324d;
      --pale: #eef6ff;
      --green: #157347;
      --red: #b42318;
      --border: #ccd9e6;
    }

    * {
      box-sizing: border-box;
    }

    html {
      scroll-behavior: smooth;
    }

    body {
      margin: 0;
      background: #f5f8fc;
      color: var(--text);
      font-family: system-ui, -apple-system, "Hiragino Kaku Gothic ProN",
                   "Yu Gothic", sans-serif;
      line-height: 1.6;
    }

    header {
      background: linear-gradient(120deg, #104b87, #287bc1);
      color: white;
      text-align: center;
      padding: 18px 16px;
    }

    header h1 {
      margin: 0 0 4px;
      font-size: clamp(1.35rem, 3vw, 2rem);
    }

    header p {
      margin: 0;
    }

    main {
      width: min(100%, 1120px);
      margin: 0 auto;
      padding: 16px;
    }

    section {
      background: white;
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 22px;
      box-shadow: 0 3px 12px #16395b0a;
    }

    [hidden] {
      display: none !important;
    }

    h2 {
      margin: 0 0 12px;
      color: #14528d;
    }

    h3 {
      margin: 14px 0 6px;
    }

    p {
      margin: 6px 0 12px;
    }

    button {
      min-height: 48px;
      border: 0;
      border-radius: 10px;
      padding: 10px 16px;
      background: var(--blue);
      color: white;
      font: inherit;
      font-weight: 700;
      cursor: pointer;
      touch-action: manipulation;
    }

    button:hover:not(:disabled) {
      background: var(--blue-dark);
    }

    button:focus-visible,
    summary:focus-visible,
    h2:focus-visible {
      outline: 3px solid #f6ba42;
      outline-offset: 3px;
    }

    button:disabled {
      cursor: default;
    }

    button.secondary {
      background: #526d83;
    }

    button.secondary:hover:not(:disabled) {
      background: #3d586d;
    }

    .small {
      color: #526579;
      font-size: 0.93rem;
    }

    /* メニュー */

    .menu-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 16px;
      margin: 18px 0;
    }

    button.menu-button {
      display: flex;
      align-items: center;
      gap: 16px;
      width: 100%;
      min-height: 125px;
      padding: 18px;
      text-align: left;
      background: var(--pale);
      color: var(--text);
      border: 2px solid #b9d5ee;
      border-radius: 14px;
    }

    button.menu-button:hover:not(:disabled) {
      background: #d9ecfc;
      color: var(--text);
    }

    .menu-icon {
      flex: 0 0 auto;
      font-size: 2.1rem;
      line-height: 1;
    }

    .menu-button strong {
      display: block;
      font-size: 1.08rem;
    }

    .menu-button small {
      display: block;
      margin-top: 4px;
      font-size: 0.88rem;
      font-weight: 400;
      color: #526579;
    }

    /* クイズ画面 */

    .screen-heading {
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-wrap: wrap;
      gap: 10px;
    }

    .screen-heading h2 {
      margin: 0;
    }

    .stats {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin: 15px 0;
    }

    .stats span {
      background: var(--pale);
      padding: 5px 12px;
      border-radius: 20px;
      font-weight: 700;
    }

    #question {
      margin: 18px 0 15px;
      font-size: clamp(1.12rem, 2vw, 1.35rem);
      font-weight: 700;
    }

    .choices {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 12px;
      margin: 14px 0;
    }

    button.choice {
      position: relative;
      width: 100%;
      min-height: 78px;
      padding: 15px 18px;
      background: #edf6ff;
      color: var(--text);
      border: 2px solid #b8d3ea;
      border-radius: 12px;
      text-align: left;
      font-size: 1.06rem;
      overflow-wrap: anywhere;
    }

    button.choice:hover:not(:disabled) {
      background: #dceeff;
      color: var(--text);
      border-color: var(--blue);
    }

    button.choice:disabled {
      opacity: 1;
    }

    button.choice.correct {
      background: #e4f7e9;
      color: #105b33;
      border-color: var(--green);
    }

    button.choice.wrong {
      background: #ffebe8;
      color: #8e2118;
      border-color: var(--red);
    }

    .choice-letter {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      width: 28px;
      height: 28px;
      margin-right: 8px;
      border-radius: 50%;
      background: #c8def2;
      font-size: 0.9rem;
    }

    .choice.correct .choice-letter {
      background: #b4e6c3;
    }

    .choice.wrong .choice-letter {
      background: #f4bcb5;
    }

    #feedback {
      padding: 13px 15px;
      margin: 14px 0;
      border-radius: 10px;
      white-space: pre-line;
      font-weight: 500;
    }

    #feedback:empty {
      display: none;
    }

    #feedback.correct {
      background: #e8f7ee;
      color: #105b33;
    }

    #feedback.wrong {
      background: #fff0ee;
      color: #8e2118;
    }

    .game-actions {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 14px;
    }

    /* 重要ポイントの確認表 */

    details {
      margin: 12px 0;
      padding: 10px 14px;
      border: 1px solid var(--border);
      border-radius: 10px;
      background: #fbfdff;
    }

    summary {
      cursor: pointer;
      font-weight: 700;
      color: #14528d;
    }

    .reference-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 10px;
      margin-top: 12px;
    }

    .reference-card {
      padding: 10px;
      background: var(--pale);
      border-left: 4px solid var(--blue);
      border-radius: 6px;
    }

    .reference-card p {
      margin: 3px 0 0;
    }

    /* iPad横向き：横幅を活かし、縦方向はコンパクトにする */

    @media (orientation: landscape) and (min-width: 768px) {
      header {
        padding: 10px 20px;
      }

      header h1 {
        font-size: 1.55rem;
      }

      main {
        padding: 12px 20px;
      }

      section {
        padding: 18px 22px;
      }

      .choices {
        gap: 10px;
      }

      button.choice {
        min-height: 70px;
      }
    }

    /* スマートフォンなどの狭い画面 */

    @media (max-width: 650px) {
      .menu-grid,
      .choices,
      .reference-grid {
        grid-template-columns: 1fr;
      }

      button.menu-button {
        min-height: 92px;
      }

      button.choice {
        min-height: 62px;
      }

      .screen-heading {
        align-items: stretch;
      }

      .screen-heading h2,
      .screen-heading button,
      .game-actions button {
        width: 100%;
      }
    }
  </style>
</head>

<body>
  <header>
    <h1>⚗️ 原子量・分子量・式量 マスターゲーム</h1>
    <p>高校化学基礎｜4枚のカードから答えを選ぼう</p>
  </header>

  <main>
    <!-- メニュー -->
    <section id="menu" aria-labelledby="menu-title">
      <h2 id="menu-title" tabindex="-1">🏠 メニュー</h2>
      <p>取り組みたい項目を選んでください。</p>

      <div class="menu-grid">
        <button type="button" id="lessonBtn" class="menu-button">
          <span class="menu-icon" aria-hidden="true">📖</span>
          <span>
            <strong>重要ポイントを学ぶ</strong>
            <small>基本事項を4択クイズで確認</small>
          </span>
        </button>

        <button type="button" id="practiceBtn" class="menu-button">
          <span class="menu-icon" aria-hidden="true">📘</span>
          <span>
            <strong>資料の問題に挑戦</strong>
            <small>ポイントチェック・EXERCISEを4択で解く</small>
          </span>
        </button>

        <button type="button" id="formulaBtn" class="menu-button">
          <span class="menu-icon" aria-hidden="true">🧩</span>
          <span>
            <strong>化学式を選ぶ</strong>
            <small>正しい添字・括弧・電荷を見分ける</small>
          </span>
        </button>

        <button type="button" id="timeBtn" class="menu-button">
          <span class="menu-icon" aria-hidden="true">⏱</span>
          <span>
            <strong>90秒タイムアタック</strong>
            <small>ランダムな12問に挑戦</small>
          </span>
        </button>
      </div>

      <p class="small">
        おすすめの順番：重要ポイント → 資料の問題 → 化学式 → タイムアタック
      </p>
    </section>

    <!-- クイズ画面：全モード共通 -->
    <section id="game" aria-labelledby="game-title" hidden>
      <div class="screen-heading">
        <h2 id="game-title" tabindex="-1">問題に挑戦</h2>
        <button type="button" id="menuBtn" class="secondary">
          ← メニューに戻る
        </button>
      </div>

      <div id="lessonReference" hidden>
        <details>
          <summary>先に重要ポイントを見る／もう一度確認する</summary>

          <div class="reference-grid">
            <div class="reference-card">
              <strong>相対質量</strong>
              <p>¹²C 原子1個の質量を12として比較した値。単位はない。</p>
            </div>

            <div class="reference-card">
              <strong>原子量</strong>
              <p>同位体の相対質量を、存在比に応じて平均した値。</p>
            </div>

            <div class="reference-card">
              <strong>分子量</strong>
              <p>分子に含まれる各原子の原子量の合計。例：H₂O＝18。</p>
            </div>

            <div class="reference-card">
              <strong>式量</strong>
              <p>組成式やイオンの化学式に含まれる各原子の原子量の合計。例：NaCl＝58.5。</p>
            </div>
          </div>
        </details>
      </div>

      <div class="stats" aria-live="off">
        <span id="progress">問題：—</span>
        <span id="score">正解：0問</span>
        <span id="timer" hidden>残り：90秒</span>
        <span id="best" hidden>自己ベスト：0問</span>
      </div>

      <div id="question"></div>
      <p id="instruction" class="small">正しい答えのカードを1枚選んでください。</p>

      <div id="choices" class="choices" role="group" aria-label="4択の解答カード"></div>

      <div id="feedback" role="status" aria-live="polite"></div>

      <div class="game-actions">
        <button type="button" id="nextBtn" hidden>次の問題へ →</button>
        <button type="button" id="restartBtn" class="secondary">
          このモードを最初から
        </button>
      </div>
    </section>
  </main>

  <script>
    "use strict";

    /*
      問題データの形式：
      q(問題番号, 問題文, 正解, [不正解1, 不正解2, 不正解3], 解説)

      表示順は各問題でシャッフルします。
      すべての問題に必ず4枚のカードを表示します。
    */
    const q = (id, text, answer, wrong, explanation) => ({
      id, text, answer, wrong, explanation
    });

    /* 重要ポイント：理解の入口となるクイズ */
    const lessonQuestions = [
      q(
        "基本1",
        "原子の相対質量を決めるとき、基準にする原子は？",
        "¹²C",
        ["¹H", "¹⁶O", "³⁵Cl"],
        "質量数12の炭素原子 ¹²C 1個の質量を12として比較します。"
      ),
      q(
        "基本2",
        "相対質量について正しい説明は？",
        "比較した値なので単位はない",
        ["単位は g", "単位は mol", "単位は %"],
        "実際の質量を g で表すのではなく、基準と比較した値なので単位はありません。"
      ),
      q(
        "基本3",
        "原子量を求めるときに考慮するものは？",
        "同位体の相対質量と存在比",
        ["陽子の存在比だけ", "原子番号だけ", "電子の速さ"],
        "同位体ごとの相対質量を、天然に存在する割合に応じて平均します。"
      ),
      q(
        "基本4",
        "35.0 の同位体が75%、37.0 の同位体が25%ある。原子量は？",
        "35.5",
        ["35.0", "36.0", "72.0"],
        "35.0×0.75＋37.0×0.25＝35.5 です。"
      ),
      q(
        "基本5",
        "水 H₂O の分子量の計算式は？",
        "1.0×2＋16＝18",
        ["1.0＋16＝17", "1.0×16×2＝32", "1.0×2＋16×2＝34"],
        "H は2個、O は1個。各原子の原子量に個数を掛けて足します。"
      ),
      q(
        "基本6",
        "NaCl の58.5を表す適切な用語は？",
        "式量",
        ["分子量", "質量数", "原子番号"],
        "NaCl は組成式で表すため、原子量の合計を式量といいます。"
      ),
      q(
        "基本7",
        "分子量を用いるのに適切な物質は？",
        "アンモニア NH₃",
        ["塩化ナトリウム NaCl", "水酸化ナトリウム NaOH", "金 Au"],
        "NH₃ は分子として表す物質なので、分子量を用います。"
      ),
      q(
        "基本8",
        "イオンの式量を求めるとき、電子の授受による質量変化は？",
        "通常は無視できる",
        ["必ず2倍する", "電荷の数だけ足す", "原子量から10を引く"],
        "電子は原子に比べて非常に軽いため、通常の式量計算では無視します。"
      )
    ];

    /* 添付資料：ポイントチェック、EXERCISE、例題 */
    const practiceQuestions = [
      q(
        "確認(1)",
        "原子量の基準となる元素は？",
        "炭素",
        ["水素", "酸素", "塩素"],
        "質量数12の炭素原子 ¹²C を基準にします。"
      ),
      q(
        "確認(2)",
        "基準となる ¹²C 原子の質量数は？",
        "12",
        ["6", "13", "24"],
        "¹²C の左肩の12が質量数です。"
      ),
      q(
        "確認(3)",
        "¹²C 原子1個の相対質量は？",
        "12",
        ["1", "6", "24"],
        "定義により、¹²C 原子1個の相対質量を12とします。"
      ),
      q(
        "確認(4)",
        "¹²C＝12 としたとき、¹H 原子の相対質量はおよそいくつ？",
        "1.0",
        ["0.1", "12", "16"],
        "¹H 原子の相対質量はおよそ1.0です。"
      ),
      q(
        "確認(5)",
        "同じ元素で、質量数の異なる原子を何という？",
        "同位体",
        ["分子", "イオン結晶", "化合物"],
        "陽子数が同じで、中性子数が異なる原子を同位体といいます。"
      ),
      q(
        "確認(6)",
        "同位体の存在比を考慮した相対質量の平均値を何という？",
        "原子量",
        ["分子量", "式量", "質量数"],
        "これが原子量の定義です。"
      ),
      q(
        "確認(7)",
        "¹²C が99%、¹³C が1%のとき、炭素の原子量は？",
        "12.01",
        ["12.00", "12.10", "13.00"],
        "12×0.99＋13×0.01＝12.01。"
      ),
      q(
        "確認(8)",
        "分子の相対質量を何という？",
        "分子量",
        ["原子番号", "質量数", "存在比"],
        "分子に含まれる原子の原子量を合計して求めます。"
      ),
      q(
        "確認(9)",
        "分子量は、構成する原子の原子量の何を求める？",
        "和",
        ["積", "差", "平均"],
        "各原子について「原子量×個数」を求め、最後に足し合わせます。"
      ),
      q(
        "確認(10)",
        "水 H₂O の分子量は？（H＝1.0、O＝16）",
        "18",
        ["17", "32", "34"],
        "1.0×2＋16＝18。"
      ),
      q(
        "確認(11)",
        "組成式やイオンの化学式から求めた原子量の総和は？",
        "式量",
        ["原子番号", "質量数", "存在比"],
        "組成式・イオンの化学式には式量を用います。"
      ),
      q(
        "確認(12)",
        "NaCl の式量は？（Na＝23、Cl＝35.5）",
        "58.5",
        ["35.5", "46.0", "81.5"],
        "23＋35.5＝58.5。"
      ),
      q(
        "確認(13)",
        "イオンの式量で、電子の授受による質量変化は無視できる？",
        "できる",
        ["できない", "陽イオンだけできる", "陰イオンだけできる"],
        "電子は原子に比べて非常に軽いため、通常は無視できます。"
      ),
      q(
        "確認(14)",
        "水酸化物イオン OH⁻ の式量は？（O＝16、H＝1.0）",
        "17",
        ["15", "16", "18"],
        "16＋1.0＝17。電荷は計算に加えません。"
      ),
      q(
        "確認(15)",
        "分子量を用いるのに適切なのは？",
        "アンモニア",
        ["金", "水酸化ナトリウム", "塩化ナトリウム"],
        "アンモニア NH₃ は分子として表す物質です。"
      ),
      q(
        "46",
        "¹²C 1個が 2.0×10⁻²³ g、Al 1個が 4.5×10⁻²³ g。Al の相対質量は？",
        "27",
        ["18", "24", "32"],
        "4.5÷2.0×12＝27。"
      ),
      q(
        "47",
        "¹⁰B が20.0%、¹¹B が80.0%。ホウ素の原子量は？",
        "10.8",
        ["10.2", "10.5", "11.0"],
        "10.0×0.200＋11.0×0.800＝10.8。"
      ),
      q(
        "48(1)",
        "窒素 N₂ の分子量は？（N＝14）",
        "28",
        ["14", "16", "42"],
        "14×2＝28。"
      ),
      q(
        "48(2)",
        "水 H₂O の分子量は？",
        "18",
        ["16", "17", "20"],
        "1.0×2＋16＝18。"
      ),
      q(
        "48(3)",
        "二酸化炭素 CO₂ の分子量は？",
        "44",
        ["28", "32", "60"],
        "12＋16×2＝44。"
      ),
      q(
        "48(4)",
        "硫酸 H₂SO₄ の分子量は？",
        "98",
        ["82", "96", "114"],
        "1.0×2＋32＋16×4＝98。"
      ),
      q(
        "48(5)",
        "グルコース C₆H₁₂O₆ の分子量は？",
        "180",
        ["168", "174", "192"],
        "12×6＋1.0×12＋16×6＝180。"
      ),
      q(
        "49(1)",
        "水酸化ナトリウム NaOH の式量は？",
        "40",
        ["39", "41", "56"],
        "23＋16＋1.0＝40。"
      ),
      q(
        "49(2)",
        "炭酸カルシウム CaCO₃ の式量は？",
        "100",
        ["84", "88", "116"],
        "40＋12＋16×3＝100。"
      ),
      q(
        "49(3)",
        "カルシウムイオン Ca²⁺ の式量は？",
        "40",
        ["38", "42", "80"],
        "電子の質量は無視するので、Ca の原子量と同じ40です。"
      ),
      q(
        "49(4)",
        "硝酸イオン NO₃⁻ の式量は？",
        "62",
        ["46", "48", "63"],
        "14＋16×3＝62。電荷は加算しません。"
      ),
      q(
        "49(5)",
        "リン酸マグネシウム Mg₃(PO₄)₂ の式量は？",
        "262",
        ["167", "191", "286"],
        "24×3＋(31＋16×4)×2＝262。括弧の外の2を忘れずに。"
      ),
      q(
        "例題50",
        "Al₂O₃ 中の Al の含有率は？（有効数字3桁）",
        "52.9%",
        ["26.5%", "47.1%", "54.0%"],
        "式量は27×2＋16×3＝102。Al の分は54なので、54÷102×100＝52.9%。"
      ),
      q(
        "50(1)",
        "酸化鉄(Ⅲ) Fe₂O₃ の式量は？",
        "160",
        ["112", "144", "176"],
        "56×2＋16×3＝160。"
      ),
      q(
        "50(2)",
        "Fe₂O₃ 中の Fe の含有率は？（有効数字3桁）",
        "70.0%",
        ["30.0%", "56.0%", "75.0%"],
        "Fe の分は56×2＝112。112÷160×100＝70.0%。"
      )
    ];

    /* 化学式：正しい添字、括弧、電荷を見分ける */
    const formulaQuestions = [
      q(
        "化学式1",
        "水の化学式は？",
        "H₂O",
        ["HO", "H₂O₂", "HO₂"],
        "水はHが2個、Oが1個です。"
      ),
      q(
        "化学式2",
        "アンモニアの化学式は？",
        "NH₃",
        ["NH₂", "N₂H₃", "NH₄"],
        "アンモニアはNが1個、Hが3個です。"
      ),
      q(
        "化学式3",
        "二酸化炭素の化学式は？",
        "CO₂",
        ["CO", "C₂O", "CO₃"],
        "「二酸化」なので、Oが2個です。"
      ),
      q(
        "化学式4",
        "塩化ナトリウムの組成式は？",
        "NaCl",
        ["Na₂Cl", "NaCl₂", "Na₂Cl₂"],
        "Na⁺ と Cl⁻ の個数比は1：1です。"
      ),
      q(
        "化学式5",
        "水酸化ナトリウムの組成式は？",
        "NaOH",
        ["Na₂OH", "NaO₂H", "Na(OH)₂"],
        "Na⁺ と OH⁻ を1：1で組み合わせます。"
      ),
      q(
        "化学式6",
        "炭酸カルシウムの組成式は？",
        "CaCO₃",
        ["Ca₂CO₃", "Ca(CO₃)₂", "CaCO₂"],
        "Ca²⁺ と CO₃²⁻ を1：1で組み合わせます。"
      ),
      q(
        "化学式7",
        "酸化アルミニウムの組成式は？",
        "Al₂O₃",
        ["AlO", "Al₃O₂", "AlO₃"],
        "Al³⁺ が2個、O²⁻ が3個で電荷がつり合います。"
      ),
      q(
        "化学式8",
        "酸化鉄(Ⅲ)の組成式は？",
        "Fe₂O₃",
        ["FeO", "FeO₂", "Fe₃O₂"],
        "Fe³⁺ が2個、O²⁻ が3個です。"
      ),
      q(
        "化学式9",
        "リン酸マグネシウムの組成式は？",
        "Mg₃(PO₄)₂",
        ["MgPO₄", "Mg₂(PO₄)₃", "Mg₃PO₄₂"],
        "Mg²⁺ が3個、PO₄³⁻ が2個です。PO₄をまとめて括弧で囲みます。"
      ),
      q(
        "化学式10",
        "硝酸イオンの化学式は？",
        "NO₃⁻",
        ["NO₂⁻", "NO₃²⁻", "NO₄⁻"],
        "Nが1個、Oが3個で、電荷は−1です。"
      )
    ];

    const $ = id => document.getElementById(id);

    let state = null;
    let timerId = null;

    function shuffle(items) {
      const result = [...items];

      for (let i = result.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [result[i], result[j]] = [result[j], result[i]];
      }

      return result;
    }

    function readBest() {
      try {
        return Number(localStorage.getItem("atomicMassCardBest") || 0);
      } catch {
        return 0;
      }
    }

    function saveBest(score) {
      try {
        localStorage.setItem("atomicMassCardBest", String(score));
      } catch {
        // 保存が制限された環境でもゲームは継続する。
      }
    }

    function stopTimer() {
      if (timerId !== null) {
        clearInterval(timerId);
        timerId = null;
      }
    }

    function showScreen(name) {
      $("menu").hidden = name !== "menu";
      $("game").hidden = name !== "game";

      const heading = name === "menu"
        ? $("menu-title")
        : $("game-title");

      heading.scrollIntoView({
        behavior: "smooth",
        block: "start"
      });
      heading.focus({ preventScroll: true });
    }

    function showMenu() {
      stopTimer();
      state = null;
      showScreen("menu");
    }

    function start(mode) {
      stopTimer();

      let questions;

      if (mode === "lesson") {
        questions = [...lessonQuestions];
      } else if (mode === "practice") {
        questions = [...practiceQuestions];
      } else if (mode === "formula") {
        questions = [...formulaQuestions];
      } else {
        questions = shuffle([
          ...lessonQuestions,
          ...practiceQuestions,
          ...formulaQuestions
        ]).slice(0, 12);
      }

      state = {
        mode,
        questions,
        index: 0,
        correct: 0,
        answered: false,
        finished: false,
        deadline: mode === "time" ? Date.now() + 90000 : null,
        remaining: 90
      };

      $("game-title").textContent = {
        lesson: "📖 重要ポイントを学ぶ",
        practice: "📘 資料の問題に挑戦",
        formula: "🧩 化学式を選ぶ",
        time: "⏱ 90秒タイムアタック"
      }[mode];

      $("lessonReference").hidden = mode !== "lesson";
      $("timer").hidden = mode !== "time";
      $("best").hidden = mode !== "time";

      showScreen("game");
      showQuestion();

      if (mode === "time") {
        timerId = setInterval(updateTimer, 200);
      }
    }

    function updateTimer() {
      if (!state || state.finished || state.mode !== "time") return;

      // 画面を切り替えて戻ってきても、実際の経過時間で計算する。
      state.remaining = Math.max(
        0,
        Math.ceil((state.deadline - Date.now()) / 1000)
      );

      $("timer").textContent = `残り：${state.remaining}秒`;

      if (Date.now() >= state.deadline) {
        finish("時間切れ！");
      }
    }

    function updateStats() {
      if (!state) return;

      $("progress").textContent =
        `問題：${Math.min(state.index + 1, state.questions.length)} / ` +
        `${state.questions.length}`;

      $("score").textContent = `正解：${state.correct}問`;
      $("timer").textContent = `残り：${state.remaining}秒`;
      $("best").textContent = `自己ベスト：${readBest()}問`;
    }

    function showQuestion() {
      if (!state || state.finished) return;

      const item = state.questions[state.index];
      state.answered = false;

      $("question").textContent = `${item.id}｜${item.text}`;
      $("instruction").hidden = false;
      $("choices").hidden = false;

      $("feedback").textContent = "";
      $("feedback").className = "";
      $("nextBtn").hidden = true;

      const choiceBox = $("choices");
      choiceBox.replaceChildren();

      const displayedChoices = shuffle([
        item.answer,
        ...item.wrong
      ]);

      displayedChoices.forEach((choice, index) => {
        const button = document.createElement("button");
        const letter = document.createElement("span");
        const label = document.createElement("span");

        button.type = "button";
        button.className = "choice";

        letter.className = "choice-letter";
        letter.setAttribute("aria-hidden", "true");
        letter.textContent = ["A", "B", "C", "D"][index];

        label.textContent = choice;

        button.append(letter, label);

        button.addEventListener("click", () => {
          chooseAnswer(choice, button);
        });

        choiceBox.append(button);
      });

      updateStats();
    }

    function chooseAnswer(selected, selectedButton) {
      if (!state || state.finished || state.answered) return;

      // タイマー表示の更新間隔より先に制限時間が来ていた場合も防ぐ。
      if (state.mode === "time" && Date.now() >= state.deadline) {
        updateTimer();
        return;
      }

      const item = state.questions[state.index];
      const isRight = selected === item.answer;

      state.answered = true;

      if (isRight) {
        state.correct++;
      }

      for (const button of $("choices").querySelectorAll("button")) {
        const choiceText = button.lastElementChild.textContent;

        button.disabled = true;

        if (choiceText === item.answer) {
          button.classList.add("correct");
        }

        if (button === selectedButton && !isRight) {
          button.classList.add("wrong");
        }
      }

      const feedback = $("feedback");
      feedback.className = isRight ? "correct" : "wrong";
      feedback.textContent = isRight
        ? `正解！\n${item.explanation}`
        : `惜しい！ 正解：${item.answer}\n${item.explanation}`;

      $("nextBtn").hidden = false;
      $("nextBtn").textContent =
        state.index === state.questions.length - 1
          ? "結果を見る →"
          : "次の問題へ →";

      updateStats();
    }

    function nextQuestion() {
      if (!state || state.finished || !state.answered) return;

      if (state.mode === "time" && Date.now() >= state.deadline) {
        updateTimer();
        return;
      }

      state.index++;

      if (state.index >= state.questions.length) {
        finish("全問題終了！");
      } else {
        showQuestion();
      }
    }

    function finish(reason) {
      if (!state || state.finished) return;

      state.finished = true;
      stopTimer();

      if (state.mode === "time") {
        state.remaining = Math.max(
          0,
          Math.ceil((state.deadline - Date.now()) / 1000)
        );

        if (state.correct > readBest()) {
          saveBest(state.correct);
        }
      }

      $("question").textContent = reason;
      $("instruction").hidden = true;
      $("choices").hidden = true;
      $("nextBtn").hidden = true;

      $("feedback").className = "correct";
      $("feedback").textContent =
        `${state.questions.length}問中、${state.correct}問正解！` +
        (state.mode === "time"
          ? ` 残り時間：${state.remaining}秒。`
          : "") +
        "\n間違えた問題の解説を思い出して、もう一度挑戦しましょう。";

      updateStats();
    }

    // メニュー
    $("lessonBtn").addEventListener("click", () => start("lesson"));
    $("practiceBtn").addEventListener("click", () => start("practice"));
    $("formulaBtn").addEventListener("click", () => start("formula"));
    $("timeBtn").addEventListener("click", () => start("time"));

    // ゲーム操作
    $("menuBtn").addEventListener("click", showMenu);
    $("nextBtn").addEventListener("click", nextQuestion);

    $("restartBtn").addEventListener("click", () => {
      if (state) start(state.mode);
    });
  </script>
</body>
</html>
