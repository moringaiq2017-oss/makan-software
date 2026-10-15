# نشر موقع مكان للبرمجيات

موقع ثابت (HTML فقط) على نفس VPS مكان `76.13.144.220` — بلا كلفة إضافية.
النطاق: `soft.makanstudios.net`

## 1) DNS — في لوحة Hostinger (makanstudios.net → DNS)
سجل جديد: `A` · الاسم `soft` · القيمة `76.13.144.220` · TTL افتراضي

## 2) على السيرفر (مرة وحدة)
```bash
git clone https://github.com/moringaiq2017-oss/makan-software.git /var/www/makan-software
cat > /etc/nginx/sites-available/makan-software <<'NG'
server {
    listen 80;
    server_name soft.makanstudios.net;
    root /var/www/makan-software;
    index index.html;
    location ~ /\.(git|md) { deny all; }
    location ~* \.(webp|png|jpg|css|js)$ { expires 30d; }
}
NG
ln -s /etc/nginx/sites-available/makan-software /etc/nginx/sites-enabled/
nginx -t && systemctl reload nginx
certbot --nginx -d soft.makanstudios.net
```

## 3) التحديث بعد أي تعديل
```bash
git -C /var/www/makan-software pull
```

## تعديل رقم الواتساب والإيميل
أعلى `<script>` في `index.html`: الثابتان `WHATSAPP` و `EMAIL`.
