---
title: "AI时代的Token经济：宏观视角机构研报"
date: 2026-04-30 10:00:00 +0800
categories: [研究, AI]
tags: [AI, Token经济, 宏观经济, 区块链, 研报]
lang: zh-CN
---

这是我尝试使用 AI 辅助完成的一份研究报告，从宏观经济学视角审视 AI 时代的 Token 经济体系——涵盖货币政策传导、市场微观结构，以及机构资本配置策略等核心议题。

报告全文如下，可在下方直接阅读，也可 [点击此处下载 PDF](/doc/ai_token_macro_report_institutional.pdf){:target="_blank"}。

---

<style>
.pdf-viewer-box {
  width: 100%;
  background: #1e1e2e;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 24px rgba(0,0,0,0.35);
  margin: 1.5rem 0;
  font-family: -apple-system, "PingFang SC", "Microsoft YaHei", sans-serif;
}
.pdf-toolbar {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 16px;
  background: #2a2a3e;
  border-bottom: 1px solid #3a3a5e;
  flex-wrap: wrap;
}
.pdf-toolbar button {
  background: #3a3a5e;
  color: #cdd6f4;
  border: none;
  border-radius: 6px;
  padding: 5px 12px;
  cursor: pointer;
  font-size: 14px;
  transition: background 0.2s;
}
.pdf-toolbar button:hover { background: #585b70; }
.pdf-toolbar button:disabled { opacity: 0.4; cursor: default; }
.pdf-page-info {
  color: #a6adc8;
  font-size: 13px;
  flex: 1;
  text-align: center;
  min-width: 80px;
}
.pdf-zoom-label {
  color: #a6adc8;
  font-size: 13px;
}
.pdf-download-btn {
  background: #313244 !important;
  color: #89dceb !important;
  text-decoration: none;
  border-radius: 6px;
  padding: 5px 12px;
  font-size: 13px;
  border: 1px solid #45475a;
  transition: background 0.2s;
}
.pdf-download-btn:hover { background: #45475a !important; }
.pdf-canvas-area {
  overflow-y: auto;
  max-height: 840px;
  background: #181825;
  padding: 16px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
}
#pdf-render-canvas {
  max-width: 100%;
  box-shadow: 0 2px 12px rgba(0,0,0,0.5);
  border-radius: 4px;
  background: #fff;
}
.pdf-loading {
  color: #a6adc8;
  padding: 48px;
  font-size: 15px;
  text-align: center;
}
.pdf-error {
  color: #f38ba8;
  padding: 32px;
  text-align: center;
  font-size: 14px;
}
</style>

<div class="pdf-viewer-box">
  <div class="pdf-toolbar">
    <button id="pdf-prev" disabled>&#8592; 上一页</button>
    <button id="pdf-next" disabled>下一页 &#8594;</button>
    <span class="pdf-page-info" id="pdf-page-info">加载中…</span>
    <button id="pdf-zoom-out" disabled>－ 缩小</button>
    <span class="pdf-zoom-label" id="pdf-zoom-label">100%</span>
    <button id="pdf-zoom-in" disabled>＋ 放大</button>
    <a class="pdf-download-btn" href="/doc/ai_token_macro_report_institutional.pdf" download>&#8595; 下载</a>
  </div>
  <div class="pdf-canvas-area" id="pdf-canvas-area">
    <div class="pdf-loading" id="pdf-loading">正在加载 PDF，请稍候…</div>
    <canvas id="pdf-render-canvas"></canvas>
  </div>
</div>

<script>
(function () {
  var PDFJS_VERSION = '3.11.174';
  var PDF_URL = '/doc/ai_token_macro_report_institutional.pdf';

  /* Inject pdf.js from CDN */
  function loadScript(src, cb) {
    var s = document.createElement('script');
    s.src = src;
    s.onload = cb;
    s.onerror = function () {
      document.getElementById('pdf-loading').className = 'pdf-error';
      document.getElementById('pdf-loading').textContent = '脚本加载失败，请检查网络后刷新页面。';
    };
    document.head.appendChild(s);
  }

  var cdnBase = 'https://cdn.jsdelivr.net/npm/pdfjs-dist@' + PDFJS_VERSION + '/build/';

  loadScript(cdnBase + 'pdf.min.js', function () {
    pdfjsLib.GlobalWorkerOptions.workerSrc = cdnBase + 'pdf.worker.min.js';

    /* Use standard fonts CDN for Chinese embedded-font fallback */
    pdfjsLib.GlobalWorkerOptions.cMapUrl = cdnBase + '../cmaps/';

    var canvas     = document.getElementById('pdf-render-canvas');
    var ctx        = canvas.getContext('2d');
    var btnPrev    = document.getElementById('pdf-prev');
    var btnNext    = document.getElementById('pdf-next');
    var btnZoomIn  = document.getElementById('pdf-zoom-in');
    var btnZoomOut = document.getElementById('pdf-zoom-out');
    var pageInfo   = document.getElementById('pdf-page-info');
    var zoomLabel  = document.getElementById('pdf-zoom-label');
    var loadingMsg = document.getElementById('pdf-loading');

    var pdfDoc    = null;
    var pageNum   = 1;
    var scale     = 1.4;
    var rendering = false;

    function renderPage(num) {
      if (rendering) return;
      rendering = true;
      pdfDoc.getPage(num).then(function (page) {
        var viewport = page.getViewport({ scale: scale });
        var dpr = window.devicePixelRatio || 1;
        canvas.width  = viewport.width  * dpr;
        canvas.height = viewport.height * dpr;
        canvas.style.width  = viewport.width  + 'px';
        canvas.style.height = viewport.height + 'px';
        ctx.setTransform(dpr, 0, 0, dpr, 0, 0);

        page.render({
          canvasContext: ctx,
          viewport: viewport
        }).promise.then(function () {
          rendering = false;
          pageInfo.textContent = '第 ' + num + ' 页 / 共 ' + pdfDoc.numPages + ' 页';
          btnPrev.disabled = (num <= 1);
          btnNext.disabled = (num >= pdfDoc.numPages);
        });
      });
    }

    function updateZoomLabel() {
      zoomLabel.textContent = Math.round(scale * 100) + '%';
    }

    btnPrev.addEventListener('click', function () {
      if (pageNum <= 1) return;
      pageNum--;
      renderPage(pageNum);
    });

    btnNext.addEventListener('click', function () {
      if (pageNum >= pdfDoc.numPages) return;
      pageNum++;
      renderPage(pageNum);
      document.getElementById('pdf-canvas-area').scrollTop = 0;
    });

    btnZoomIn.addEventListener('click', function () {
      if (scale >= 3.0) return;
      scale = Math.round((scale + 0.2) * 10) / 10;
      updateZoomLabel();
      renderPage(pageNum);
    });

    btnZoomOut.addEventListener('click', function () {
      if (scale <= 0.4) return;
      scale = Math.round((scale - 0.2) * 10) / 10;
      updateZoomLabel();
      renderPage(pageNum);
    });

    pdfjsLib.getDocument({
      url: PDF_URL,
      cMapUrl: 'https://cdn.jsdelivr.net/npm/pdfjs-dist@' + PDFJS_VERSION + '/cmaps/',
      cMapPacked: true
    }).promise.then(function (pdf) {
      pdfDoc = pdf;
      loadingMsg.style.display = 'none';
      btnPrev.disabled  = true;
      btnNext.disabled  = (pdf.numPages <= 1);
      btnZoomIn.disabled  = false;
      btnZoomOut.disabled = false;
      updateZoomLabel();
      renderPage(pageNum);
    }).catch(function (err) {
      loadingMsg.className = 'pdf-error';
      loadingMsg.textContent = 'PDF 加载失败：' + err.message + '。请尝试直接下载查看。';
    });
  });
})();
</script>

---

> **说明**：本报告由 AI 辅助生成，仅供学习研究使用，不构成投资建议。
{: .prompt-warning }
