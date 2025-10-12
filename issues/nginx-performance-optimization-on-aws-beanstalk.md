# ⚡ Optimizing Website Performance with Custom Nginx Configuration on AWS Elastic Beanstalk

### 🧩 Problem
Our website deployed on **AWS Elastic Beanstalk** needed improved performance scores and faster page load times.  

However:
- **Default Nginx configuration** did not have compression enabled (gzip or Brotli).  
- Multiple online tutorials suggested adding settings under `.ebextensions/`, but none of them actually applied to the Beanstalk Nginx instance.  
- Security and compression headers were missing, impacting both **SEO ranking** and **Core Web Vitals**.

---

### ⚙️ Environment & Tools
- **AWS Elastic Beanstalk (Node.js Platform)**  
- **Nginx** (Reverse proxy managed by Beanstalk)  
- **Custom configuration in `.platform/nginx/` directory**  
- **Compression:** Gzip + Brotli  
- **Security headers:** HSTS, X-Frame-Options, X-Content-Type-Options, etc.

---

### 🛠️ Solution
After experimenting with various configurations, the final working setup required placing the **custom Nginx configuration** inside:.platform/nginx/nginx.conf

----

### 📈 Impact
✅ Improved website loading speed by ~25–30%
✅ Increased Google PageSpeed Insights and Lighthouse scores
✅ Enhanced SEO ranking through better performance metrics
✅ Strengthened security posture by adding standard HTTP headers

----

### 🧾 Key Takeaways

**Not all Beanstalk configurations apply equally*** — the .platform/nginx/ path overrides the managed proxy layer, making it the right place for Nginx-level changes.

***Compression + headers*** not only boost performance but also reduce TTFB (Time to First Byte) and enhance browser caching efficiency.

This change required deep platform debugging, going beyond generic documentation to find what truly worked in production.
