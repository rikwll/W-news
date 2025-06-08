# W-news
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>w-news</title>
    <style>
        /* Estilos básicos */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
            color: #333;
        }

        header {
            background-color: #007bff;
            color: white;
            padding: 1rem;
            text-align: center;
        }

        main {
            padding: 2rem;
        }

        h1 {
            margin: 0;
            font-size: 2rem;
        }

        #news-container article {
            background: white;
            margin: 1rem 0;
            padding: 1rem;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        #news-container h2 {
            margin: 0 0 0.5rem;
            font-size: 1.5rem;
        }

        #news-container p {
            margin: 0 0 1rem;
            color: #666;
        }

        #news-container a {
            text-decoration: none;
            color: #007bff;
            font-weight: bold;
        }

        #news-container a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <header>
        <h1>Últimas Notícias</h1>
    </header>
    <main>
        <div id="news-container">
            <p>Carregando notícias...</p>
        </div>
    </main>
    <script>
        const newsContainer = document.getElementById('news-container');

        async function fetchNews() {
            // URL da API do GNews (exemplo com top-headlines)
            const apiUrl = 'https://gnews.io/api/v4/top-headlines?apikey=b3e198de8250d7911fc33570502a4e9a';

            try {
                const response = await fetch(apiUrl);

                if (!response.ok) {
                    throw new Error(`Erro na API: ${response.status} - ${response.statusText}`);
                }

                const data = await response.json();

                // Limpa o container antes de adicionar notícias
                newsContainer.innerHTML = '';

                // Adiciona as notícias ao HTML
                data.articles.forEach(article => {
                    const newsArticle = document.createElement('article');
                    newsArticle.innerHTML = `
                        <h2>${article.title}</h2>
                        <p>${article.description || 'Descrição não disponível.'}</p>
                        <a href="${article.url}" target="_blank">Leia mais</a>
                    `;
                    newsContainer.appendChild(newsArticle);
                });
            } catch (error) {
                console.error('Erro ao buscar notícias:', error);
                newsContainer.innerHTML = '<p>Não foi possível carregar as notícias. Tente novamente mais tarde.</p>';
            }
        }

        // Carrega as notícias ao iniciar
        fetchNews();
    </script>
</body>
</html>


