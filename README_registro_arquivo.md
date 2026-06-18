# 📚 Livro Digital de Arquivamento de Provas · FMC

Sistema institucional para registro, consulta e controle do arquivamento físico de provas da Faculdade de Medicina de Campos.

---

## Descrição

Substitui o livro físico de controle de provas por uma solução digital completa. Permite registrar cada prova aplicada — com dados da disciplina, professor, colaborador, quantidade arquivada, localização física e status — e gerar relatórios em PDF para fins institucionais e auditorias.

---

## Funcionalidades

### Dashboard
- **Estatísticas em tempo real**: total de registros, provas arquivadas, pendências e devoluções
- **Tabela de registros recentes** com acesso rápido aos últimos lançamentos
- **Mini calendário** com navegação por mês e marcação de dias com eventos
- **Relógio** com hora de Brasília

### Registro de provas (formulário)
Cada registro contém:

| Campo | Descrição |
|-------|-----------|
| Disciplina | Nome da matéria avaliada |
| Período | 1º ao 8º período do curso |
| Tipo de prova | PA1, PA2, Suplementar, Repositiva etc. |
| Data e horário | Data de aplicação da prova |
| Semestre | Semestre letivo de referência |
| Professor responsável | Docente titular da disciplina |
| Colaborador | Servidor ou monitor responsável pelo arquivamento |
| Quantidade | Número de provas arquivadas |
| Local físico | Identificação do local de guarda (pasta, gaveta, arquivo) |
| Status | Arquivada / Pendente / Devolvida |
| Observações | Campo livre para anotações |
| Assinaturas | Canvas para assinatura digital ou campo de nome |

### Navegação por períodos
- Visualização das disciplinas organizadas por período (1º ao 8º)
- Cards por disciplina mostrando todos os registros vinculados
- Atalhos rápidos na barra lateral para cada período

### Busca e filtros
- **Busca textual** por disciplina, professor, colaborador ou observação
- **Filtros por status**: Arquivada, Pendente, Devolvida
- **Relatórios filtrados** por período, tipo de prova, semestre ou status

### Relatórios
- **Relatório geral** — todos os registros
- **Por período** — provas de um período específico
- **Por status** — somente arquivadas, pendentes ou devolvidas
- **Por semestre** — agrupamento por semestre letivo
- Exportação dos relatórios em **PDF** (paisagem A4) com cabeçalho institucional

### Exportação e backup
- **Exportar PDF** de um registro individual ou do relatório completo
- **Imprimir** registro individual com campos de assinatura física
- **Backup JSON** — exporta todos os dados para arquivo local
- **Importar JSON** — restaura dados a partir de backup
- **Limpar dados** — apaga todos os registros (com confirmação)

---

## Persistência de dados

O sistema suporta dois modos de armazenamento, configuráveis no início do arquivo:

### Firebase Firestore (padrão)
- Dados sincronizados em nuvem em tempo real
- Múltiplos usuários podem acessar e atualizar simultaneamente
- Requer configuração das credenciais do projeto Firebase no bloco `firebaseConfig`

### localStorage (fallback)
- Dados salvos localmente no navegador
- Funciona sem internet e sem configuração adicional
- Os dados ficam restritos ao dispositivo e navegador

---

## PWA — Instalação como Aplicativo

Este arquivo está configurado como **Progressive Web App** e pode ser instalado no dispositivo para acesso rápido como um aplicativo nativo.

### Requisitos
- Hospedagem via **HTTPS** (GitHub Pages, Netlify etc.)
- Navegador: Chrome, Edge ou Samsung Internet

### Estrutura de arquivos

```
pwa_registro/
├── index.html       ← Aplicativo principal
├── manifest.json    ← Configuração do PWA
├── sw.js            ← Service Worker (cache offline)
├── icon-192.png     ← Ícone para tela inicial
└── icon-512.png     ← Ícone para splash screen
```

### Deploy no GitHub Pages

1. Faça upload de todos os arquivos da pasta `pwa_registro/` para um repositório público no GitHub
2. Acesse **Settings → Pages** e habilite na branch `main`
3. Acesse a URL HTTPS gerada
4. O banner de instalação aparecerá automaticamente no Chrome/Edge

### Comportamento offline

O Service Worker usa estratégia **Network-First** com cache de fallback. Requisições ao Firebase Firestore passam direto pela rede (não são interceptadas) para garantir a integridade dos dados em tempo real. Os recursos estáticos (HTML, fontes, bibliotecas) são cacheados na primeira carga e ficam disponíveis offline.

---

## Tecnologias

- HTML5 / CSS3 / JavaScript puro (sem frameworks)
- Fontes: [Playfair Display](https://fonts.google.com/specimen/Playfair+Display) + [DM Sans](https://fonts.google.com/specimen/DM+Sans)
- [Firebase Firestore](https://firebase.google.com/docs/firestore) — sincronização em nuvem
- [jsPDF](https://github.com/parallax/jsPDF) + [jsPDF-AutoTable](https://github.com/simonbengtsson/jsPDF-AutoTable) — geração de PDF
- Canvas API — assinatura digital
- PWA: Web App Manifest + Service Worker

---

## Configuração Firebase

Para ativar a sincronização em nuvem, localize o bloco `firebaseConfig` no início do `<script>` e preencha com as credenciais do seu projeto Firebase:

```javascript
const firebaseConfig = {
  apiKey: "SUA_API_KEY",
  authDomain: "seu-projeto.firebaseapp.com",
  projectId: "seu-projeto",
  storageBucket: "seu-projeto.appspot.com",
  messagingSenderId: "000000000000",
  appId: "1:000000000000:web:abcdef123456"
};
```

As credenciais estão disponíveis no [Console do Firebase](https://console.firebase.google.com/) em **Configurações do projeto → Seus aplicativos**.

---

## Instituição

**Faculdade de Medicina de Campos (FMC)**  
Campos dos Goytacazes — RJ  
Uso interno — Setor de Controle Acadêmico
