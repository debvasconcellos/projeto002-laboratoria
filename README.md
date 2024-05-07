# PROJETO 2 - FICHA TÉCNICA

# Ficha Técnica: Projeto Análise de Dados 2

## Título do Projeto: Hipóteses Spotify 🎶

---

## Objetivo

Num mundo onde a **indústria musical** é extremamente competitiva e em constante evolução, a capacidade de tomar decisões baseadas em dados tornou-se um ativo inestimável.

Neste contexto, uma gravadora enfrenta o emocionante desafio de lançar um novo artista no cenário musical global. Felizmente, ela tem uma ferramenta poderosa em seu arsenal: um extenso conjunto de dados do Spotify com informações sobre as músicas mais ouvidas em 2023.

- A gravadora levantou uma série de hipóteses sobre o que faz uma música seja mais ouvida. Essas hipóteses incluem:
- Músicas com BPM (Batidas Por Minuto) mais altos fazem mais sucesso em termos de número de streams no Spotify.
- As músicas mais populares no ranking do Spotify também possuem um comportamento semelhante em outras plataformas, como a Deezer.
- A presença de uma música em um maior número de playlists está correlacionada com um maior número de streams.
- Artistas com um maior número de músicas no Spotify têm mais streams.
- As características da música influenciam o sucesso em termos de número de streams no Spotify.

Você deve validar (refutar ou confirmar) essas hipóteses através da análise de dados e fornecer recomendações estratégicas com base em suas descobertas. O objetivo principal desta análise é que a gravadora e o novo artista possam tomar decisões informadas que aumentem suas chances de alcançar o “sucesso”.

---

## Equipe

Dupla (Ana Guimarães e Débora Vasconcellos)

---

## Ferramentas e Tecnologias

- BigQuery
- Power BI
- Google Colab

Linguagens: SQL e Python

---

## Processamento e Análises

---

### Limpeza dos dados

### **Valores nulos**

***Tabela “track_in_competition”***

50 registros nulos na variável ‘in_shazam_charts’, optamos por retirar a variável por entendermos que o Shazam não é uma plataforma de streaming, mas sim, um aplicativo buscador de canções. Dessa forma, não é uma variável relevante para os objetivos do projeto.

- ***Tabela “track_in_spotify”***

2 casos de ‘track_name’ vazios após a remoção de caracteres especiais. Optamos por manter as faixas e as renomeamos pelo texto ‘nao identificado’. 

- ***Tabela “track_technical_info”***

95 casos nulos na variável ‘**key**’, optamos por retirar essa variável conjuntamente com a variável “Mode”, por entendermos que não são variáveis importantes para os objetivos do projeto. 

- ***Tabela “track_in_spotify_clean”***

1 nulo na variável “streams”, optamos por removê-lo por ser apenas um caso e essa variável ser importante para o objetivo do projeto.

1 caso discrepante na variável “released_year”, observamos que a track_id 2475712 tinha seu ano de lançamento errado e optamos por alterar a data. “01/01/1930” para “10/10/2022”

---

### Valores duplicados

- ***Tabela “track_in_spotify”***

***colunas:** track_name, artist_s__name*

4 registros 

| SNAP | Rosa Linn |
| --- | --- |
| About Damn Time | Lizzo |
| Take My Breath | The Weeknd |
| SPIT IN MY FACE! | ThxSoMch |

Decidimos selecionar os casos priorizando aqueles que tinham informação no “in_spotify_charts”, já que algumas músicas tinham essa informação registrada enquanto suas cópias não tinham. Entendemos que a posição no ranking spotify é uma informação importante para os objetivos do projeto. 

- ***Tabela “track_in_competition” e Tabela “track_technical_info”***

Não foram encontrados valores duplicados.

---

### **Caracteres Especiais e Alteração do tipo da variável**

- ***Tabela “track_in_spotify_clean”***

Aplicada remoção de caracteres especiais e aplicação de letras minúsculas nas variáveis “track_name” e “artist_s__name”.

Alteração do tipo de variável de STRING para INTEGER na variável “streams”.

Após alteração da variável “streams”, identificamos um caso que estava em formato de texto e após transformação foi transformado em nulo e removido.

---

### Novas variáveis e tabelas

### Variáveis Gerais

### **Nova Tabela “full_table_spotify”**

“**release_date_concat**”: Através da fórmula CONCAT geramos a data completa de lançamento da música.

”**release_year_month_concat**”: Através da fórmula CONCAT geramos Ano-Mês de lançamento da música como uma variável.

”**total_playlists**”: Somatório da presença da música em playlists de todas as plataformas de streaming analisadas (spotify, deezer, apple music)

---

### Nova Tabela “artist-count-streams”

**“total_musicas”**: Somatório de todas as músicas mais tocadas em 2023 no spotify por artista. 

**“total_streams”**: Somatório dos streams de todas as músicas por artista.

---

### Variáveis para Segmentação

Para analisarmos se havia diferença entre as características mais altas e baixas da música (bpm, danceability, energy, etc) e no número de streams das canções. Precisamos dividir as variáveis em quartis, em seguida categorizamos o 4º quartil como Alto e os demais quartis como Baixo. Optamos pela divisão 25% Alto e 75% Baixo para concentrar os casos altos que eram o foco das nossas validações de hipóteses.  Dessa forma foram criadas as seguintes variáveis:

### **Nova Tabela “full_table_spotify_quartis”**

**“bpm_quartil” e “bpm_categorizada”**: Primeiro dividimos a variável em quartis e após a divisão categorizamos o quartil 4 como “Alto” e os demais quartis como “Baixo”. 

**“danceability_quartil” e “danceability_categorizada”**: Primeiro dividimos a variável em quartis e após a divisão categorizamos o quartil 4 como “Alto” e os demais quartis como “Baixo”. 

**“valence_quartil” e “valence_categorizada”**: Primeiro dividimos a variável em quartis e após a divisão categorizamos o quartil 4 como “Alto” e os demais quartis como “Baixo”. 

**“energy_quartil” e “energy_categorizada”**: Primeiro dividimos a variável em quartis e após a divisão categorizamos o quartil 4 como “Alto” e os demais quartis como “Baixo”. 

**“acousticness_quartil” e “acousticness_categorizada”**: Primeiro dividimos a variável em quartis e após a divisão categorizamos o quartil 4 como “Alto” e os demais quartis como “Baixo”. 

**“instrumentalness_quartil” e “instrumentalness_categorizada”**: Primeiro dividimos a variável em quartis e após a divisão categorizamos o quartil 4 como “Alto” e os demais quartis como “Baixo”. 

**“liveness_quartil” e “liveness_categorizada”**: Primeiro dividimos a variável em quartis e após a divisão categorizamos o quartil 4 como “Alto” e os demais quartis como “Baixo”. 

**“speechiness_quartil” e “speechiness_categorizada”**: Primeiro dividimos a variável em quartis e após a divisão categorizamos o quartil 4 como “Alto” e os demais quartis como “Baixo”. 

---

### Validação de Hipóteses

- **Métodos Estatísticos**:
- Medidas de tendência central - Observadas através das ferramentas de visualização do Power BI
- Testes de Correlação - No Google Colab com linguagem Python foram realizados os testes: **R de Pearson** e **Spearman**
- Teste de amostras independentes - No Google Colab com Linguagem Python foi realizado o teste **U de Mann-Whitney**
- Regressão Linear Simples - No Google Colab foram realizados com Linguagem Python a regressão do **total_playlists + streams**, de **bpm + streams**, de **released_year + streams** e de **total_musicas + total_streams**.

---

### Gráficos

- Histograma (Visualizar a distribuição através)
- Dispersão (Observar a distribuição dos casos com linha de tendência)
- Matrix de Correlação (Mapa de calor com os resultados obtidos nos testes de correlação)

---

## Resultados e Conclusões

### Hipótese 1

**Músicas com BPM (Batidas Por Minuto) mais altos fazem mais sucesso em termos de streams no Spotify - HIPÓTESE REFUTADA**

- Através dos histogramas e medidas de tendência central das variáveis, percebemos que ambas não apresentam uma distribuição normal. Dessa forma, optamos pelo teste não paramétrico U de Mann-Whitney para avaliar se havia diferença entre os grupos de BPM Alto e Baixo.
- No resultado do teste podemos inferir que não há base para rejeitarmos a hipótese nula, ou seja, não há significância estatística para afirmarmos que há diferença entre quantidade de Streams e valores Altos X Baixos do BPM. (p-value > 0,05)
- Quando olhamos para o gráfico de dispersão e a linha de tendência, conjuntamente com o R de Pearson e r² da regressão linear, percebemos que BPM não possui efeito de causalidade no aumento de streams, assim como essas variáveis não possuem correlação alguma.
- BPM (Batidas por Minuto) é uma medida que mensura a velocidade rítmica. Na produção musical, BPM é uma ferramenta que pode auxiliar os artistas na construção de suas identidades musicais. Isso é possível devido a presenças rítmicas marcantes que acabam sendo associadas a determinados gêneros e subgêneros musicais. Por exemplo: Hip-hop tem suas batidas entre 60-100 bpm, enquanto o Techno/trance fica em torno de 120-140 bpm. Dessa forma, BPM pode ser uma variável interessante se pensada em conjunto com as variáveis gênero e subgênero musical.
- Fontes: [Tempo e gênero musical | Learning Music (ableton.com)](https://learningmusic.ableton.com/pt/make-beats/tempo-and-genre.html)

[Entenda o conceito e a importância do "BPM" na música eletrônica (b2bportal.com.br)](https://b2bportal.com.br/conceito-e-significado-de-bpm/)

- RESUMO: BPM Alto não influencia no sucesso de Streams.

---

### Hipótese 2

**As músicas mais populares no ranking do Spotify também possuem um comportamento semelhante em outras plataformas como Deezer - HIPÓTESE CONFIRMADA**

- Entendemos que as variáveis analisadas possuem um nível de mensuração ordinal, já que correspondem a posição das músicas nos rankings de cada plataforma de stream.
- Dessa forma, optamos pelo teste de correlação de Spearman em detrimento do R de Pearson, já que o primeiro é um teste não paramétrico que se baseia no "rank" das variáveis, e não nos valores exatos. Enquanto o R de Pearson, mede a força de uma relação linear entre duas variáveis contínuas.
- Com os resultados obtidos, podemos afirmar que há uma correlação positiva moderada estatisticamente significativa tanto entre os charts do Spotify e da Apple, quanto do Spotify e da Deezer.
- Atualmente, o Spotify lidera o mercado brasileiro. A Deezer se encontra em segundo lugar na escolha dos usuários brasileiros, enquanto a Apple Music é o segundo lugar para os consumidores estadounidenses.
- Fontes: [Spotify mantém liderança de mercado nos EUA e Apple Music vem na sequência, aponta relatório - TudoCelular.com](https://www.tudocelular.com/mercado/noticias/n208351/spotify-mantem-lideranca-mercado-eua-relatorio.html#:~:text=De%20acordo%20com%20o%20levantamento,quase%2012%20milh%C3%B5es%20a%20menos.)
- [O que é streaming? Descubra as 8 maiores plataformas de 2024 (netshow.me)](https://netshow.me/blog/mas-o-que-e-streaming/)
- RESUMO: Os rankings apresentam comportamento semelhante moderado. Não há efeito de causalidade do Spotify para com as demais plataformas, mas há uma tendência para um comportamento correlato.

---

### Hipótese 3

**A presença de uma música em um maior número de playlists é relacionada a um maior número de streams - HIPÓTESE PARCIALMENTE CONFIRMADA**

- O número de playlists que uma canção pode ser encontrada no Spotify e o número de streams dela são variáveis contínuas que podem ter sua correlação testada através do R de Pearson.
- Realizamos o R de Pearson conjuntamente com a técnica de regressão linear e percebemos que, apesar de uma correlação positiva forte (0,78), o p-valor e coeficiente r² demonstram que essa relação entre as variáveis não é suficiente para um efeito de causalidade. Portanto, número em playlists é uma variável que, sozinha, não consegue explicar o crescimento de números em streams.
- Segundo Geovane Bento, Diretor da LEP Music Brasil, as próprias playlists do Spotify possuem uma certa divisão para o aplicativo. Há as Playlists Editoriais, Personalizadas, de Usuários e Outras Fontes. Seria interessante complementar essa análise com os dados referentes aos comportamentos de streams de acordo com os tipos de playlists.
- Fontes: [Como Crescer as Audições no Spotify: Estratégias Comprovadas | LinkedIn](https://www.linkedin.com/pulse/como-crescer-audi%C3%A7%C3%B5es-spotify-estrat%C3%A9gias-comprovadas-geovane-bento-lpjzf/)
- [Tipos de playlists do Spotify - Spotify](https://support.spotify.com/br-pt/artists/article/types-of-spotify-playlists/)
- RESUMO: Presença em mais playlists e um maior número de streams se apresenta com uma correlação positiva forte, porém não há efeito de causalidade suficiente para que a regressão linear tenha uma capacidade de previsibilidade robusta.

---

### Hipótese 4

**Artistas com maior número de músicas no Spotify têm mais streams - HIPÓTESE PARCIALMENTE CONFIRMADA**

- Quando observamos o gráfico de dispersão, percebemos que a maioria dos casos se concentra entre artistas com 1 - 5 músicas. Apenas uma artista, a Taylor Swift, tem mais de 30 músicas entre as 948 mais ouvidas em 2023.
- Apesar da evidente ausência de normalidade, decidimos realizar a regressão linear para entender de forma mais complexa a possível causalidade do total de músicas e o número de streams.
- O resultado do R de Pearson nos indica que há uma correlação positiva forte entre total de músicas e streams, entretanto o p-valor e o coeficiente r² nos indicam que não há significância estatística suficiente para defendermos a causalidade entre as variáveis. Portanto, apesar de haver uma relação entre maior número de músicas e mais streams, não podemos assumir que a causa do número elevado de streams se dê somente pela maior presença de músicas.
- Artistas com mais de 5 músicas nas mais ouvidas de 2023 são poucos quando observamos o todo. Artistas como a Taylor Swift e o The Weekend são, literalmente, pontos fora da curva que se destoam da maioria. Seria interessante observar suas estratégias de marketing, financiamentos de suas gravadoras, além de outras questões que possam ajudar a compreender os motivos que levam ao desempenho acima da média que possuem.
- Fontes: [Taylor Swift bate recorde no Spotify com 'Tortured poets department', disco mais ouvido em um só dia na plataforma | Música | G1 (globo.com)](https://g1.globo.com/pop-arte/musica/noticia/2024/04/19/taylor-swift-bate-recorde-no-spotify-com-tortured-poets-department-disco-mais-ouvido-em-um-so-dia-na-plataforma.ghtml)
- [The Weeknd bate recorde de streams no Spotify (terra.com.br)](https://www.terra.com.br/diversao/musica/the-weeknd-bate-recorde-de-streams-no-spotify,2b920956ee98553b78f7657f81d48b3ae8y1qt7d.html)
- RESUMO: Maior número de músicas de artistas tem uma correlação positiva forte com número de streams, mas não há um efeito de causalidade estatisticamente significativo.

---

### Hipótese 5

**As características da música influenciam no sucesso em termos de streams no Spotify - HIPÓTESE REFUTADA**

- Através da matrix de correlação, percebemos que as características da música não apresentavam uma correlação estatisticamente significativa.
- Com a divisão das características das músicas em grupos de Alta e Baixa presença, optamos por realizar o teste U de Mann-Whitney para aferir se havia um comportamento diferente entre os grupos e o número de streams das canções.
- A partir do teste, encontramos apenas duas características que havia uma diferença estatisticamente significativa entre os grupos, que foram as características: Danceability e Speechines. Quando observamos o teste de correlação, percebemos que as duas apresentam um valor de -0,11. Esse valor indicaria uma correlação negativa muitíssimo fraca.
- Dessa forma, refutamos a hipótese devido a falta de provas que sustentem que as características influenciam no número de streams.
- Porém, seria interessante observar as características das músicas e a influência que podem exercer na repercussão da canção dentro do seu gênero e subgênero musical.
- RESUMO: As características das músicas não influenciam diretamente no sucesso em termos de streams.

---

### Sugestões

- CONHEÇA AS PLATAFORMAS: Entenda como o Spotify, Deezer, Apple Music, entre outros serviços de streaming, organizam os seus charts e a exposição de músicas em suas playlists. Spotify, atualmente, é a plataforma com maior destaque no setor o que torna suas escolhas seguidas por suas concorrentes. Entretanto, há algumas particularidade, por exemplo, o serviço de som Dolby Atmos (tecnologia mais atual e de melhor qualidade sonora) só está disponível nas plataformas Apple Musica, Tidal e Amazon Music Unlimited.
- CONHEÇA O SEU GÊNERO: O cenário musical possui múltiplos gêneros e subgêneros que possuem características musicais diferentes. Momentos históricos refletem na presença ou ausência de certos ritmos no consumo mais popular, entretanto, cada gênero tem seu nicho e artistas podem ter um forte grupo de ouvintes mesmo que não atinjam as primeiras posições nos charts.
- CRIE VÍNCULOS COM O SEU PÚBLICO: A relação com os ouvintes é fundamental. Comunique muito bem quem você é, quais são suas referências musicais, quando serão seus shows e forme uma rede de seguidores. Dentro do seu gênero e subgênero haverá ouvintes de outros artistas que podem ter afinidade com o seu som. Tanto sua canção pode ser recomendada pela plataforma em decorrência do histórico de consumo daquele determinado tipo de ouvinte, como pode ser indicada por playslists editoriais do gênero. Então é muito importante saber se comunicar com esse público construindo uma relação que torne suas novidades o interesse desses ouvintes.
- TRATE PLAYLISTS COMO AMPLIFICADORES: As playlists são os espaços em que suas canções serão reproduzidas e ouvidas por muitas pessoas. As playlists editoriais são importantes espaços criados pelo Spotify para divulgar determinadas músicas inseridas em determinados temas, ritmos, gêneros, etc. Entendendo o perfil do artista, as gravadoras podem direcionar seus materiais para o spotify indicando quais playlists podem ser interessantes. Além disso, há o crescimento orgânico dentro da sua rede de seguidores. Os ouvintes que seguem o seu perfil terão a oportunidade de ouvir suas músicas em playlists criadas para o usuário como "Release Radar" e "Discover Weekly". A Release Radar recomenda as músicas lançadas recentemente pelos artistas seguidos pelo usuário, enquanto a Discover Weekly apresenta músicas novas ou antigas do artista que o algoritmo indica que não foram escutadas ainda pelo usuário.
- Fontes:
- [Como funciona o algoritmo do Spotify? Truques de streaming para músicos (dittomusic.com)](https://dittomusic.com/pt/blog/how-does-spotifys-algorithm-work-streaming-hacks-for-musicians)
- [Como colocar sua música no Discover Weekly e no Release Radar (dittomusic.com)](https://dittomusic.com/pt/blog/how-to-get-your-music-on-discover-weekly-and-release-radar)
- [Apple Music pode pagar mais para artistas que usarem Dolby Atmos – Tecnoblog](https://tecnoblog.net/noticias/apple-music-pode-pagar-mais-para-artistas-que-usarem-dolby-atmos/#:~:text=O%20Apple%20Music%20tem%20suporte,n%C3%A3o%20conta%20com%20a%20tecnologia.)
- [Playlists editoriais do Spotify: passo a passo de como entrar (groover.co)](https://blog.groover.co/pt/dicas-para-musicos/playlists-editoriais-spotify/#2_Qual_a_importancia_das_playlists_editoriais)
- [Estudo de caso Spotify: a disrupção no streaming de músicas - G4 Educacão (g4educacao.com)](https://g4educacao.com/portal/case-spotify)
- [Como ouvintes impactam no sucesso de artistas através do Spotify | Exame](https://exame.com/casual/como-ouvintes-impactam-no-sucesso-de-artistas-atraves-do-spotify/)

---

## Limitações/Próximos Passos

### **Limitações:**

1. **Amostra de Dados:** A análise pode ser limitada pela disponibilidade e qualidade dos dados do Spotify. Nesse caso, estávamos apenas com as 948 músicas mais tocadas globalmente no Spotify em 2023. Para mais inferências, entender os cases de menor sucesso também poderia agregar informações por contraste.  Além disso, se a amostra não for representativa o suficiente, as conclusões podem não ser generalizáveis.
2. **Correlação não implica causalidade:** Encontrar correlações entre variáveis não significa necessariamente que uma causa a outra. É importante interpretar os resultados com cautela e considerar outras variáveis não incluídas na análise. Como por exemplo: gênero e sub gênero musical, origem cultural étnica, são variáveis utilizadas pelo algoritmo do Spotify para recomendações aos usuários. Poderiam ter um efeito de causalidade conjunta com a presença em playlists. 
3. **Falta de Linha Temporal:** Seria interessante ter o desempenho das músicas ao longo dos meses. Assim, poderíamos tentar entender o comportamento de crescimento dos streams em cada período. 
4. **Variáveis não consideradas:** Existem muitas outras variáveis que podem influenciar o sucesso de uma música no Spotify, como marketing, promoção, eventos ao vivo, entre outros. Além disso, identidade de gênero do artista, quantitativo de presença em playlists editoriais e de usuários, poderiam agregar mais informações para análise. Essas variáveis não foram incluídas no escopo. 

### **Próximos Passos:**

1. **Incluir e Validar Dados Externos:** Incorporar dados externos, como informações demográficas dos ouvintes ou tendências de mídia social, para enriquecer a análise e obter insights adicionais. Assim como, validar a análise utilizando dados de outras fontes ou períodos de tempo, para verificar se os padrões observados são consistentes. 
2. **Aprofundamento nas Hipóteses:** Investigar cada hipótese de forma mais detalhada, agregando outras variáveis que podem ter efeito de causalidade promovendo uma análise mais robusta para validação das hipóteses.
3. **Feedback do Artista:** Obter feedback dos artistas sobre as descobertas e ajustar as estratégias de lançamento com base nesse feedback.
4. **Avaliação de Métricas de Sucesso Alternativas:** Além do número de streams, explorar outras métricas de sucesso, como engajamento do usuário ou conversões em vendas de álbuns ou ingressos de shows.

---

## Links de interesse

Github:

Google Colab:

[Google Colab](https://colab.research.google.com/drive/1oKcHaF7ROJ3hp2auwhVCIWDdbWtnxGMs?usp=sharing)

[Google Colab](https://colab.research.google.com/drive/1KDlF_7hDtZcjJq9SCO2ABN95_M45Xodp?usp=sharing)

Dashboards Power BI: 
https://drive.google.com/file/d/1F58I_QV7m2A0PQPooYIY2M2afwGw14bC/view?usp=sharing 

https://drive.google.com/file/d/1rhSR1RTUVbL5y28KzmcoA5wISuWXDRrN/view?usp=sharing

Apresentação Slides:

https://docs.google.com/presentation/d/134fd0cRt3o7M8z03gilCGxrsX4Q12DFIED5aQzSXMBY/edit?usp=sharing

---

---