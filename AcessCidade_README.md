# 🏙️ AcessCidade - Guia de Projeto (README)

## 🎯 Objetivo do Protótipo

Entregar uma **aplicação web navegável** (sem backend real) onde o usuário pode:

1. Ver um mapa ou lista de locais acessíveis  
2. Pesquisar por categoria ou tipo de acessibilidade  
3. Cadastrar / favoritar locais (dados simulados)  
4. Visualizar detalhes de um local  
5. Fazer login fake (apenas validação simples com e-mail/senha)

---

## 🧩 Divisão em 3 Módulos (1 por integrante)

| Módulo | Responsável sugerido | Descrição | Tecnologias principais |
|--------|----------------------|------------|--------------------------|
| 1️⃣ Estrutura & Navegação | **Jorge** | Configurar projeto React, rotas, Navbar, Footer, Layout principal, roteamento entre páginas | React + Vite + React Router |
| 2️⃣ UI & Componentes | **Yasmin** | Criar os componentes de interface (Card, Botão, Formulário, Modal, etc.), seguindo estilo visual dos slides | Tailwind ou CSS Modules |
| 3️⃣ Funcionalidades básicas | **Savio** | Criar Contexto de Favoritos e de Usuário (mock), implementar listagem e filtro dos locais, e página de detalhes | React Context API + LocalStorage |

---

## 🧱 Estrutura mínima de pastas

```plaintext
src/
 ├── components/
 │    ├── Navbar.tsx
 │    ├── Footer.tsx
 │    ├── Card.tsx
 │    ├── Button.tsx
 │    └── Input.tsx
 ├── pages/
 │    ├── Home.tsx
 │    ├── Detalhes.tsx
 │    ├── Login.tsx
 │    ├── Cadastro.tsx
 │    └── Sobre.tsx
 ├── context/
 │    ├── UserContext.tsx
 │    └── FavoritesContext.tsx
 ├── data/
 │    └── locais.json
 ├── routes/
 │    └── index.tsx
 ├── App.tsx
 └── main.tsx
```

---

## 📋 Backlog Kanban (para o GitHub Project)

### 🟩 Semana 1 – Estrutura e Navegação
- [ ] Criar projeto React + Vite + TypeScript  
- [ ] Instalar e configurar React Router  
- [ ] Criar Navbar e Footer  
- [ ] Criar página Home (lista de locais do `locais.json`)  
- [ ] Criar layout principal com `<Outlet />`

### 🟨 Semana 2 – UI e Componentes
- [ ] Criar componente **Card** (imagem, título, tipo de acessibilidade, botão Favoritar)  
- [ ] Criar componentes de formulário reutilizáveis (**Input**, **Button**)  
- [ ] Página **Detalhes** com informações do local  
- [ ] Página **Login/Cadastro** (somente UI)

### 🟦 Semana 3 – Estado e Interações
- [ ] Criar **Contexto de Usuário** (mock login)  
- [ ] Criar **Contexto de Favoritos** (add/remove/localStorage)  
- [ ] Criar página **Favoritos**  
- [ ] Implementar **busca e filtro** na Home  

### 🟧 Semana 4 – Refinamento e Apresentação
- [ ] Revisar **acessibilidade** (semântica, foco, contraste)  
- [ ] Testar **navegação completa**  
- [ ] Inserir **prints e demo no README**  
- [ ] Preparar **pitch/slide** para o evento  

---

## 💡 Exemplo mínimo de uma funcionalidade (Favoritar)

### Antes (lógica dentro do componente)
```tsx
function Card({ local }) {
  const [favorito, setFavorito] = useState(false)

  return (
    <div>
      <h3>{local.nome}</h3>
      <button onClick={() => setFavorito(!favorito)}>
        {favorito ? "★" : "☆"}
      </button>
    </div>
  )
}
```

### Depois (com Contexto de Favoritos)

```tsx
// context/FavoritesContext.tsx
import { createContext, useContext, useState } from "react"

const FavoritesContext = createContext(null)

export function FavoritesProvider({ children }) {
  const [favorites, setFavorites] = useState<string[]>([])

  const toggleFavorite = (id: string) =>
    setFavorites(favs =>
      favs.includes(id) ? favs.filter(f => f !== id) : [...favs, id]
    )

  return (
    <FavoritesContext.Provider value={{ favorites, toggleFavorite }}>
      {children}
    </FavoritesContext.Provider>
  )
}

export const useFavorites = () => useContext(FavoritesContext)
```

```tsx
// components/Card.tsx
import { useFavorites } from "@/context/FavoritesContext"

export function Card({ local }) {
  const { favorites, toggleFavorite } = useFavorites()
  const isFav = favorites.includes(local.id)

  return (
    <div className="card">
      <h3>{local.nome}</h3>
      <button onClick={() => toggleFavorite(local.id)}>
        {isFav ? "★" : "☆"}
      </button>
    </div>
  )
}
```

---

## 🗓️ Cronograma rápido de estudos (14 dias)

| Dia | Tópico | Atividade |
|-----|---------|------------|
| 1–2 | React básico | Criar projeto, componentes e props |
| 3–4 | React Router | Navegar entre páginas |
| 5–6 | Estado e Context API | Usar `useState` e `createContext` |
| 7–8 | Componentização | Criar Card, Button, Input |
| 9–10 | Simulação de dados | Ler JSON local e mapear lista |
| 11–12 | Acessibilidade e UX | Testar navegação por teclado |
| 13–14 | Pitch + README | Revisar e preparar a apresentação |

---

## 📚 Referências recomendadas

- [MDN – HTML semântico e acessibilidade](https://developer.mozilla.org/pt-BR/docs/Learn/Accessibility)  
- [React Docs – Using Context](https://react.dev/reference/react/useContext)  
- [Vite + React Template](https://vitejs.dev/guide/)  
- [React Router 6 – Guia oficial](https://reactrouter.com/en/main/start/tutorial)  
- [W3C – Quick Reference WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)

---

## ✅ Sugestão de Metas Internas (para acompanhamento no Obsidian)

- [ ] Estrutura inicial do projeto criada  
- [ ] Navbar e Footer prontos  
- [ ] Página Home exibe lista de locais mockados  
- [ ] Contexto de Favoritos funcional  
- [ ] Interface de Login/Cadastro criada  
- [ ] Página de Detalhes exibindo informações do local  
- [ ] Favoritar funcionando em toda a navegação  
- [ ] Acessibilidade básica revisada  
- [ ] Apresentação e README finalizados
