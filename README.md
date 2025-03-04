# FunCaptcha 求解器  

[![Promo](https://github.com/luminati-io/LinkedIn-Scraper/raw/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner.png)](https://www.bright.cn/products/web-unlocker/captcha-solver/funcaptcha)

使用 Bright Data 的高级 CAPTCHA 求解技术轻松绕过 FunCaptcha。通过机器学习算法、[自动 IP 轮换](https://www.bright.cn/solutions/rotating-proxies)以及强大的代理基础设施，实现对目标站点的无缝且稳定访问。

Bright Data 的 CAPTCHA Solver 功能内置于 [**抓取浏览器**](https://www.bright.cn/products/scraping-browser) 和 [**网络解锁器 API**](https://www.bright.cn/products/web-unlocker) 中，能够轻松处理最复杂的 CAPTCHA 挑战。

## 功能特性  
- **快速求解 CAPTCHA**：可自动、高精度且高速地解决 FunCaptcha。  
- **IP 轮换**：通过自动重试和动态 IP 调整来避免封禁。  
- **浏览器指纹模拟**：模拟真实用户行为，以[绕过高阶的机器人检测](https://www.bright.cn/blog/web-data/anti-scraping-techniques)。  
- **JavaScript 渲染**：针对大量使用 JavaScript 的网站，轻松处理动态内容。  
- **全球覆盖**：精确定位，解锁任何地区的内容。  
- **无缝集成**：可与 Puppeteer、Playwright 和 Selenium 等工具轻松合作。  
- **事件监控**：追踪 CAPTCHA 求解事件，如检测、成功或失败等。

## 为什么要选择 FunCaptcha 求解器  

### **赢得超过 20,000+ 全球客户的信赖**  
Bright Data 的 CAPTCHA Solver 深受开发者、企业和大型组织的信赖，其可靠性和高性能无可比拟。

### **依托优质代理网络**  
凭借超过 1 亿个 IP 资源以及强大的地理定位能力，我们的代理基础设施可确保流畅不中断的 CAPTCHA 求解体验。

### **AI 驱动的 CAPTCHA 求解**  
CAPTCHA Solver 利用先进的 AI 逻辑自动检测、分析并求解 CAPTCHA。它会处理重试、指纹模拟以及请求头设置，成功绕过最强大的反机器人措施。

### **专为开发者打造**  
- 轻松与 Puppeteer、Playwright 和 Selenium 集成。  
- 完全可自定义的 CAPTCHA 求解参数。  
- 自动重试与动态 IP 调整，确保爬取流程不中断。

> **专业提示 💡**  
>> 已经有自己的 CAPTCHA 求解方案？结合我们的 [Puppeteer](https://www.bright.cn/integration/puppeteer)、[Playwright](https://www.bright.cn/integration/playwright) 和 [Selenium](https://www.bright.cn/integration/selenium) 代理，进一步降低遇到 CAPTCHA 的概率。

## 工作原理  

Bright Data 的 CAPTCHA Solver 集成在 **Scraping Browser** 和 **Web Unlocker** 中，让你可以轻松解决各类 CAPTCHA。

### **自动求解 CAPTCHA**  
CAPTCHA Solver 会自动检测并实时求解 CAPTCHA。只需启用该功能，即可从检测到求解全程自动化处理。

### **FunCaptcha 专用自定义选项**  
```javascript
// 为不同类型的 CAPTCHA 定义默认选项
function getCaptchaOptions(captchaType, customOptions = {}) {
  const defaultOptions = {
    timeout: 30000, // 等待 CAPTCHA 求解的最大时间（毫秒）
    check_timeout: 500, // 检查 CAPTCHA 状态的时间间隔（毫秒）
    wait_networkidle: { timeout: 1000 }, // 等待网络空闲 1 秒
    debug: false // 调试模式（默认为关闭）
  };

  // 定义不同 CAPTCHA 类型的选择器
  const captchaSelectors = {
    DataDome: { selector: '#datadome-captcha', success_selector: '#captcha-success' },
    reCAPTCHA: { selector: '.g-recaptcha', success_selector: '.recaptcha-success' },
    ClickCaptcha: { selector: '.click-captcha', success_selector: '.captcha-passed' },
    hCaptcha: { selector: '.h-captcha', success_selector: '.hcaptcha-success' },
    PerimeterX: { selector: '#px-captcha', success_selector: '#px-success' },
    SimpleCaptcha: { selector: '.simple-captcha', success_selector: '.captcha-done' },
    FunCaptcha: { selector: '.funcaptcha', success_selector: '.funcaptcha-success' },
    CloudflareTurnstile: { selector: '.cf-turnstile', success_selector: '.cf-success' },
    AWSWAF: { selector: '#aws-waf-captcha', success_selector: '#aws-waf-success' },
    GeeTest: { selector: '.geetest-captcha', success_selector: '.geetest-success' },
    KeyCAPTCHA: { selector: '#keycaptcha', success_selector: '#keycaptcha-success' },
    PuzzleCAPTCHA: { selector: '.puzzle-captcha', success_selector: '.puzzle-solved' },
    YandexCAPTCHA: { selector: '#yandex-captcha', success_selector: '#yandex-success' },
    ImageCAPTCHA: { selector: '.image-captcha', success_selector: '.image-captcha-success' },
    TextCAPTCHA: { selector: '.text-captcha', success_selector: '.text-captcha-success' }
  };

  // 获取指定 CAPTCHA 类型的选择器
  const selectedOptions = captchaSelectors[captchaType] || {};

  // 合并默认选项、CAPTCHA 类型特定选项和自定义选项
  return { ...defaultOptions, ...selectedOptions, ...customOptions };
}

// 不同 CAPTCHA 类型的示例用法
const ddOptions = getCaptchaOptions('DataDome', { timeout: 40000, debug: true });
const recaptchaOptions = getCaptchaOptions('reCAPTCHA', { debug: true });
const hcaptchaOptions = getCaptchaOptions('hCaptcha');

console.log(ddOptions);
console.log(recaptchaOptions);
console.log(hcaptchaOptions);

// 示例错误处理
try {
  if (!document.querySelector(ddOptions.selector)) {
    throw new Error(`使用选择器 ${ddOptions.selector} 未找到 CAPTCHA 元素`);
  }

  // 此处编写你的 CAPTCHA 求解逻辑
  solveCaptcha(ddOptions);
} catch (error) {
  console.error('CAPTCHA 求解失败：', error.message);
}
```

#### 示例流程：  
1. **检测 CAPTCHA**：求解器识别到 CAPTCHA 类型（如 PerimeterX）。  
2. **求解 CAPTCHA**：借助 AI 逻辑，求解器完成 CAPTCHA 的解析与认证。  
3. **失败重试**：若求解失败，系统会自动切换新的 IP 进行重试。  
4. **返回结果**：CAPTCHA 求解完成后，系统可顺畅访问目标站点。

## 支持的 CAPTCHA 类型  

Bright Data 的 CAPTCHA Solver 支持多种常见 CAPTCHA，包括：  

- [**DataDome**](https://www.bright.cn/products/web-unlocker/captcha-solver/datadome)
- [**reCAPTCHA**](https://www.bright.cn/products/web-unlocker/captcha-solver/recaptcha)
- [**Click Captcha**](https://www.bright.cn/products/web-unlocker/captcha-solver/click-captcha)
- [**Cloudflare**](https://www.bright.cn/products/web-unlocker/captcha-solver/Cloudflare)
- [**PerimeterX**](https://www.bright.cn/products/web-unlocker/captcha-solver/perimeterx)
- [**SimpleCaptcha**](https://www.bright.cn/products/web-unlocker/captcha-solver/simplecaptcha)
- [**FunCaptcha**](https://www.bright.cn/products/web-unlocker/captcha-solver/funcaptcha)
- [**Cloudflare Turnstile**](https://www.bright.cn/products/web-unlocker/captcha-solver/cloudflare-turnstile)
- [**AWS WAF Captcha**](https://www.bright.cn/products/web-unlocker/captcha-solver/aws-waf-captcha)
- [**GeeTest CAPTCHA**](https://www.bright.cn/products/web-unlocker/captcha-solver/geetest-captcha)
- [**KeyCAPTCHA**](https://www.bright.cn/products/web-unlocker/captcha-solver/keycaptcha)
- [**Puzzle CAPTCHA**](https://www.bright.cn/products/web-unlocker/captcha-solver/puzzle-captcha)
- [**Yandex CAPTCHA**](https://www.bright.cn/products/web-unlocker/captcha-solver/yandex-captcha)
- [**Image CAPTCHA**](https://www.bright.cn/products/web-unlocker/captcha-solver/image-captcha)
- [**Text CAPTCHA**](https://www.bright.cn/products/web-unlocker/captcha-solver/text-captcha)

## 高级自定义  

[Bright Data 的 CAPTCHA Solver](https://github.com/luminati-io/Captcha-solver) 提供丰富的高级自定义功能，可针对特定使用场景进行调整和优化。

## **事件监控**  
可追踪 CAPTCHA 求解事件，以应对高阶的使用场景：  
- `Captcha.detected`: 检测到 CAPTCHA 并开始求解。  
- `Captcha.solveFinished`: 成功完成 CAPTCHA 求解。  
- `Captcha.solveFailed`: CAPTCHA 求解失败。  

## **价格方案**  

| **方案**          | **价格（每 1K 结果）** | **月度费用**   | **描述**                                     |  
|-------------------|------------------------|----------------|----------------------------------------------|  
| **按量付费**       | $1.50                 | 无需长期订阅   | 适合临时或不定期的爬取需求。                  |  
| **Growth**        | $1.27                 | $499           | 专为扩展规模的团队设计。                     |  
| **Business**      | $1.12                 | $999           | 适用于大规模爬取项目。                        |  
| **Premium**       | $1.05                 | $1,999         | 提供高级功能与优先支持。                      |  
| **Enterprise**    | 定制报价               | 联系我们       | 为顶级企业需求定制专属方案。                  |  

🚀 **特别优惠**: 首次充值可享受最高至 **$500** 的充值金额对等赠送！

## **开发者爱上 FunCaptcha 求解器的原因**  
- **便捷集成**：与 Puppeteer、Playwright 和 Selenium 无缝配合。  
- **先进的 AI 逻辑**：自动执行重试、CAPTCHA 求解、指纹模拟、IP 轮换以及高级请求头设置。  
- **内置浏览器**：无需自行管理外部浏览器的 JavaScript 渲染。  
- **实时洞察**：通过实时仪表板监控网络表现。  
- **顶级支持**：提供 24/7 全天候全球客户支持，不断增添新功能。  

## **常见问题**  

### **FunCaptcha 求解器的工作原理是什么？**  
求解器使用先进的 AI 逻辑自动检测并求解 FunCaptcha。

### **它能同时处理多个 CAPTCHA 吗？**  
是的，该方案可扩容处理多种 CAPTCHA，确保访问过程不中断。

### **如果 CAPTCHA 求解失败怎么办？**  
系统会自动进行重试。如果问题仍无法解决，可联系我们的 24/7 支持团队获得帮助。  

---

## **告别 FunCaptcha 的烦恼**  
立即开始免费试用，体验与 Bright Data 一起[轻松解决 FunCaptcha](https://www.bright.cn/products/web-unlocker/captcha-solver/funcaptcha) 的畅快流程吧！  
