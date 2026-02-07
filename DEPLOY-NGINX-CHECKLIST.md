# ✅ CHECKLIST DE MIGRAÇÃO PARA NGINX/UBUNTU - COMPLETO

## 📋 Resumo das Alterações Realizadas

### 1. ✅ **Case-Sensitivity - VERIFICADO**

- **Status**: Todos os arquivos estão em lowercase ou com capitalização consistente
- **Arquivos verificados**:
  - ✅ `favicon.svg` (minúsculo)
  - ✅ `logo-hero-branco.svg` (minúsculo)
  - ✅ `logo-navbar.svg` (minúsculo)
  - ✅ `logo-mobile.webp` (minúsculo)
  - ✅ `mountains-mobile.webp` (minúsculo)
  - ✅ `mountains-trees-mesa-grande-morning-light-san-diego.webp` (minúsculo)
  - ✅ `mountains-trees-mesa-grande-morning-light-san-diego.jpg` (minúsculo)
  - ✅ `photo-mobile.webp` (minúsculo)
  - ✅ `photo-psicologo.webp` (minúsculo)
  - ✅ `photo-psicologo.jpg` (minúsculo)
  - ⚠️ `FONTES-LOCAIS-README.md` (maiúsculo - mas é apenas documentação, não afeta o site)

- **Chamadas no HTML/CSS**: Todas as referências estão em lowercase e correspondem aos nomes reais dos arquivos

### 2. ✅ **Caminhos Root-Relative - ATUALIZADOS**

Todos os caminhos foram ajustados para funcionar na raiz do domínio `www.psimatheuszanete.com.br`:

**Arquivos atualizados:**

- ✅ `/css/fonts.css` (era: `css/fonts.css`)
- ✅ `/style.css` (era: `style.css`)
- ✅ `/particles.min.js` (era: `particles.min.js`)
- ✅ `/particles-init.js` (era: `particles-init.js`)

**Já estavam corretos:**

- ✅ `/favicon.svg`
- ✅ `/logo-hero-branco.svg`
- ✅ `/logo-navbar.svg`
- ✅ `/logo-mobile.webp`
- ✅ `/mountains-mobile.webp`
- ✅ `/mountains-trees-mesa-grande-morning-light-san-diego.webp`
- ✅ `/photo-psicologo.webp`
- ✅ `/photo-mobile.webp`

### 3. ✅ **Fontes Locais - JÁ CONFIGURADAS**

**Status**: Migração completa para fontes locais já estava implementada!

**Localização**: `/css/fonts.css`
**Fontes incluídas**:

- ✅ Cinzel Regular (400)
- ✅ Cinzel SemiBold (600)
- ✅ Outfit Light (300)
- ✅ Outfit Regular (400)
- ✅ Outfit Medium (500)
- ✅ Outfit SemiBold (600)

**Configuração**:

```css
@font-face {
    font-family: 'Cinzel';
    font-display: swap; /* ✅ Otimizado para performance */
    src: url('../fonts/cinzel-v26-latin-regular.woff2') format('woff2');
}
```

**Arquivos de fonte** (todos em `/fonts/`):

- ✅ `cinzel-v26-latin-600.woff2` (15KB)
- ✅ `cinzel-v26-latin-regular.woff2` (14KB)
- ✅ `outfit-v15-latin-300.woff2` (14KB)
- ✅ `outfit-v15-latin-500.woff2` (14KB)
- ✅ `outfit-v15-latin-600.woff2` (14KB)
- ✅ `outfit-v15-latin-regular.woff2` (14KB)

**Google Fonts removido**: ✅ Não há chamadas externas no `<head>`

### 4. ✅ **Metadados - JÁ ATUALIZADOS**

**Canonical Tag**:

```html
<link rel="canonical" href="https://www.psimatheuszanete.com.br">
```

**Open Graph Tags**:

```html
<meta property="og:url" content="https://www.psimatheuszanete.com.br">
<meta property="og:image" content="https://www.psimatheuszanete.com.br/photo-psicologo.webp">
```

**Twitter Cards**:

```html
<meta property="twitter:url" content="https://www.psimatheuszanete.com.br">
<meta property="twitter:image" content="https://www.psimatheuszanete.com.br/photo-psicologo.webp">
```

**Schema.org**:

```json
{
  "@context": "https://schema.org",
  "url": "https://www.psimatheuszanete.com.br",
  "logo": "https://www.psimatheuszanete.com.br/logo-navbar.svg",
  "image": "https://www.psimatheuszanete.com.br/photo-psicologo.webp"
}
```

### 5. ✅ **Preparação para Nginx - COMPLETO**

**Arquivo `.gitignore` criado**:

- ✅ Ignora `node_modules/`, `.DS_Store`, logs, etc.
- ✅ **IMPORTANTE**: Pasta `fonts/` e imagens **NÃO** estão no `.gitignore`
- ✅ Todos os assets necessários serão incluídos no `git push`

**Dependências do GitHub Pages**:

- ✅ Não há dependências específicas do GitHub Pages
- ✅ Site é 100% estático (HTML, CSS, JS)
- ✅ Compatível com qualquer servidor web (Nginx, Apache, etc.)

---

## 🚀 PRÓXIMOS PASSOS PARA DEPLOY NO UBUNTU/NGINX

### 1. **Git Push**

```bash
git add .
git commit -m "Preparação para deploy em servidor Ubuntu/Nginx"
git push origin main
```

### 2. **Configuração do Nginx (no servidor Ubuntu)**

Crie o arquivo de configuração do site:

```bash
sudo nano /etc/nginx/sites-available/psimatheuszanete.com.br
```

**Configuração recomendada**:

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name www.psimatheuszanete.com.br psimatheuszanete.com.br;

    root /var/www/psimatheuszanete.com.br;
    index index.html;

    # Gzip compression
    gzip on;
    gzip_vary on;
    gzip_min_length 1024;
    gzip_types text/plain text/css text/xml text/javascript application/javascript application/xml+rss application/json image/svg+xml;

    # Cache static assets
    location ~* \.(jpg|jpeg|png|gif|ico|css|js|svg|webp|woff2)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    # Main location
    location / {
        try_files $uri $uri/ =404;
    }

    # Security headers
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
}
```

### 3. **Ativar o site e SSL**

```bash
# Ativar o site
sudo ln -s /etc/nginx/sites-available/psimatheuszanete.com.br /etc/nginx/sites-enabled/

# Testar configuração
sudo nginx -t

# Reiniciar Nginx
sudo systemctl restart nginx

# Instalar SSL com Certbot (HTTPS)
sudo certbot --nginx -d www.psimatheuszanete.com.br -d psimatheuszanete.com.br
```

### 4. **Upload dos arquivos**

```bash
# No servidor Ubuntu
cd /var/www/
sudo git clone <seu-repositorio> psimatheuszanete.com.br

# Ou via SFTP/SCP
scp -r * usuario@servidor:/var/www/psimatheuszanete.com.br/
```

### 5. **Permissões corretas**

```bash
sudo chown -R www-data:www-data /var/www/psimatheuszanete.com.br
sudo chmod -R 755 /var/www/psimatheuszanete.com.br
```

---

## ✅ CHECKLIST FINAL PRÉ-DEPLOY

- [x] Todos os caminhos são root-relative (`/arquivo.ext`)
- [x] Fontes locais configuradas com `font-display: swap`
- [x] Sem chamadas externas ao Google Fonts
- [x] Metadados atualizados para domínio oficial
- [x] `.gitignore` criado (assets incluídos no push)
- [x] Case-sensitivity verificada (todos os arquivos em lowercase)
- [x] Sem dependências do GitHub Pages
- [x] Site 100% estático e pronto para Nginx

---

## 📊 PERFORMANCE ESPERADA

**PageSpeed Insights**:

- ✅ Fontes locais (sem bloqueio de renderização)
- ✅ `font-display: swap` (evita FOIT)
- ✅ Imagens WebP otimizadas
- ✅ Preload de assets críticos
- ✅ Gzip habilitado no Nginx
- ✅ Cache de assets estáticos (1 ano)

**Estimativa**: 90+ no mobile e desktop após deploy com SSL e Gzip

---

## 🔍 VERIFICAÇÕES PÓS-DEPLOY

Após o deploy, verifique:

1. **Fontes carregando corretamente**:
   - Abra DevTools → Network → Filter: Font
   - Verifique se `cinzel` e `outfit` estão carregando de `/fonts/`

2. **Imagens carregando**:
   - Todas as imagens devem carregar sem erro 404
   - Verifique case-sensitivity (Linux é sensível!)

3. **CSS e JS**:
   - `/style.css` deve carregar
   - `/css/fonts.css` deve carregar
   - `/particles.min.js` e `/particles-init.js` devem carregar

4. **SSL/HTTPS**:
   - Certifique-se de que o site redireciona HTTP → HTTPS
   - Verifique se não há mixed content warnings

5. **Performance**:
   - Teste no PageSpeed Insights
   - Verifique GTmetrix
   - Teste em dispositivos móveis reais

---

## 📝 NOTAS IMPORTANTES

1. **Linux é case-sensitive**: `Foto.jpg` ≠ `foto.jpg`
   - ✅ Todos os arquivos já estão em lowercase

2. **Nginx serve arquivos da raiz**: Caminhos devem começar com `/`
   - ✅ Todos os caminhos já foram ajustados

3. **Fontes locais**: Reduzem latência e melhoram PageSpeed
   - ✅ Já configuradas e otimizadas

4. **Git push**: Certifique-se de que `fonts/` e imagens estão no repositório
   - ✅ `.gitignore` configurado corretamente

---

**Status**: ✅ **PRONTO PARA DEPLOY**

Você pode fazer o `git push` agora e seguir os passos de configuração do Nginx no servidor Ubuntu.
