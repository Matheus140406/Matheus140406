<h1 align="left">Olá, sou o Matheus! 👋</h1>

<p align="left">
  <a href="https://git.io/typing-svg">
    <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=22&pause=1000&color=F7DF1E&center=true&vCenter=true&width=500&lines=Ol%C3%A1%2C+sou+o+Matheus!;Desenvolvedor+Fullstack+em+forma%C3%A7%C3%A3o;Aprendendo+Java+e+Python;Sempre+codando+algo+novo+%F0%9F%9A%80" alt="Typing SVG" />
  </a>
</p>

<img src="https://komarev.com/ghpvc/?username=Matheus140406&label=Visualiza%C3%A7%C3%B5es+do+perfil&color=f7df1e&style=flat" align="right" />

## 👤 Perfil Profissional

- 💻 **Foco atual:** Desenvolvimento Fullstack
- 🎓 **Formação:** Sistemas de Informação (em andamento)
- 🌍 **Localização:** Brasil
- ⚡ **Curiosidade:** sempre buscando aprender algo novo em tecnologia

## 🌐 Front-end

<p align="left">
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" />
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" />
  <img src="https://img.shields.io/badge/JAVASCRIPT-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" />
</p>

## 🔙 Futuro Back-end

<p align="left">
  <img src="https://img.shields.io/badge/JAVA-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white" />
  <img src="https://img.shields.io/badge/PYTHON-3776AB?style=for-the-badge&logo=python&logoColor=white" />
</p>

## 📊 Estatísticas do GitHub

<p align="left">
  <img height="165" src="https://github-readme-stats.vercel.app/api?username=Matheus140406&show_icons=true&theme=radical&hide_border=true&count_private=true" />
  <img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=Matheus140406&layout=compact&theme=radical&hide_border=true" />
</p>

## 🔥 Sequência de Contribuições (Streak)

<p align="left">
  <img src="https://github-readme-streak-stats.herokuapp.com/?user=Matheus140406&theme=radical&hide_border=true" />
</p>

## 📈 Gráfico de Atividade (Commits)

<p align="left">
  <img src="https://github-readme-activity-graph.vercel.app/graph?username=Matheus140406&theme=react-dark&hide_border=true" />
</p>

## 🏆 Troféus

<p align="left">
  <img src="https://github-profile-trophy.vercel.app/?username=Matheus140406&theme=radical&no-frame=true&row=1&column=6" />
</p>

## 📫 Conecte-se comigo

<p align="left">
  <a href="https://github.com/Matheus140406" target="_blank">
    <img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white" />
  </a>
  <a href="https://www.linkedin.com/in/matheus-carvalho-dias-829877357/" target="_blank">
    <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" />
  </a>
  <a href="https://www.instagram.com/teamdevmatheus?igsh=OXJtMWZwNGFqY2l3" target="_blank">
    <img src="https://img.shields.io/badge/-Instagram-%23E4405F?style=for-the-badge&logo=instagram&logoColor=white" />
  </a>
  <a href="mailto:devteam2026tech@gmail.com">
    <img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white" />
  </a>
</p>

#!/bin/bash
# =========================================================
# commit-massa.sh
# Faz um commit separado para cada arquivo modificado/novo
# no repositório atual, e depois envia tudo (push) de uma vez.
# =========================================================
#
# Uso:
#   ./commit-massa.sh "mensagem base"
#
# Exemplo:
#   ./commit-massa.sh "update"
#   -> gera commits como: "update: index.html", "update: style.css", etc.
#
# Se nenhuma mensagem for passada, usa "update" como padrão.

MSG=${1:-"update"}
BRANCH=$(git branch --show-current)

# Verifica se está dentro de um repositório git
if ! git rev-parse --is-inside-work-tree > /dev/null 2>&1; then
  echo "❌ Este diretório não é um repositório git."
  exit 1
fi

echo "📦 Repositório detectado. Branch atual: $BRANCH"
echo "🔍 Verificando arquivos modificados..."

# Pega a lista de arquivos modificados/novos/deletados
ARQUIVOS=$(git status --porcelain | awk '{print $2}')

if [ -z "$ARQUIVOS" ]; then
  echo "✅ Nada para commitar. Tudo já está atualizado."
  exit 0
fi

CONTADOR=0

# Faz um commit por arquivo
while IFS= read -r arquivo; do
  if [ -n "$arquivo" ]; then
    git add "$arquivo"
    git commit -m "$MSG: $arquivo" --quiet
    if [ $? -eq 0 ]; then
      CONTADOR=$((CONTADOR + 1))
      echo "✅ Commit criado para: $arquivo"
    fi
  fi
done <<< "$ARQUIVOS"

echo ""
echo "📊 Total de commits criados: $CONTADOR"

# Pergunta antes de enviar pro remoto
read -p "🚀 Deseja enviar (push) para o repositório remoto agora? (s/n): " RESPOSTA

if [[ "$RESPOSTA" == "s" || "$RESPOSTA" == "S" ]]; then
  git push origin "$BRANCH"
  echo "🎉 Push concluído para a branch '$BRANCH'."
else
  echo "⏸️  Commits criados localmente. Envie manualmente quando quiser com: git push origin $BRANCH"
fi
