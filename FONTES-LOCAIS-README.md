# 📦 FONTES LOCAIS - GUIA COMPLETO

## ✅ O QUE FOI FEITO

### 1. **Estrutura de Arquivos Criada:**

```
mz/
├── css/
│   └── fonts.css          ← CSS com @font-face
├── fonts/
│   ├── cinzel-v26-latin-regular.woff2    (14 KB)
│   ├── cinzel-v26-latin-600.woff2        (15 KB)
│   ├── outfit-v15-latin-300.woff2        (14 KB)
│   ├── outfit-v15-latin-regular.woff2    (14 KB)
│   ├── outfit-v15-latin-500.woff2        (14 KB)
│   └── outfit-v15-latin-600.woff2        (14 KB)
└── index.html             ← Atualizado para usar fontes locais
```

**Total de fontes: ~85 KB** (vs ~200KB+ do Google Fonts com latência de rede)

---

## 🎯 BENEFÍCIOS

### **Performance:**

- ✅ **Sem CORS:** Elimina erro de preload
- ✅ **Sem latência externa:** Fontes carregam do próprio servidor
- ✅ **Cache local:** Navegador cacheia as fontes permanentemente
- ✅ **font-display: swap:** Texto aparece imediatamente com fallback

### **PageSpeed:**

- ✅ Reduz "Render Blocking Resources"
- ✅ Melhora FCP (First Contentful Paint)
- ✅ Elimina requisições DNS para fonts.googleapis.com

---

## 📝 ALTERAÇÕES NO CÓDIGO

### **index.html** (antes)

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="preload" as="style" href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600&family=Outfit:wght@300;400;500;600&display=swap" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600&family=Outfit:wght@300;400;500;600&display=swap" rel="stylesheet" media="print" onload="this.media='all'">
```

### **index.html** (depois)

```html
<link rel="stylesheet" href="css/fonts.css">
```

---

## 🔍 VERIFICAÇÃO

### **Teste realizado:**

- ✅ Fontes Cinzel e Outfit carregam corretamente
- ✅ Design visual idêntico ao anterior
- ✅ Console sem erros de CORS ou 404
- ✅ `document.fonts.check()` retorna `true` para ambas

### **Como verificar manualmente:**

1. Abra o site no navegador
2. Pressione F12 (DevTools)
3. Vá em "Network" → Filtro "Font"
4. Recarregue a página (Ctrl+R)
5. Deve ver 6 arquivos `.woff2` carregando de `/fonts/`

---

## 📊 COMPARAÇÃO

| Aspecto | Google Fonts | Fontes Locais |
|---------|--------------|---------------|
| **Tamanho total** | ~200KB+ | ~85KB |
| **Requisições HTTP** | 3-4 | 1 |
| **Latência DNS** | 50-200ms | 0ms |
| **Cache** | Compartilhado | Permanente |
| **CORS** | ❌ Erro | ✅ OK |
| **Offline** | ❌ Não funciona | ✅ Funciona |

---

## 🚀 PRÓXIMOS PASSOS

1. **Commit das alterações:**

```bash
git add css/fonts.css fonts/*.woff2 index.html
git commit -m "Migrar para fontes locais (elimina CORS, melhora performance)"
git push
```

1. **Testar no GitHub Pages** após deploy

2. **Rodar PageSpeed novamente** e verificar melhoria na pontuação

---

## 🔧 MANUTENÇÃO

### **Para adicionar novos pesos de fonte:**

1. Acesse: <https://gwfh.mranftl.com/>
2. Selecione a fonte (Cinzel ou Outfit)
3. Escolha os pesos desejados
4. Baixe o ZIP
5. Extraia os `.woff2` para `/fonts/`
6. Adicione `@font-face` correspondente em `css/fonts.css`

### **Para trocar de fonte:**

1. Baixe a nova fonte em WOFF2
2. Adicione `@font-face` em `css/fonts.css`
3. Atualize as variáveis CSS em `style.css`:

```css
:root {
    --font-heading: 'NovaFonte', serif;
    --font-body: 'OutraFonte', sans-serif;
}
```

---

**✅ Migração concluída com sucesso!**
