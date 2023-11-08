# Saga do erro CS5001 do GCP 
O problema do 5001 (CSC : error CS5001: Program does not contain a static 'Main' method suitable for an entry point) não tem relação com o erro informado.
Também não tem relação com o ERROR: build step 0 "gcr.io/cloud-builders/docker" failed: step exited with non-zero status: 1.
Por fim não tem nada a ver com The command '/bin/sh -c dotnet build "projeto.csproj" -c Release -o /app/build' returned a non-zero code: 1

## A solução para o problema é:
De certa forma simples e ao mesmo tempo complexo, porque não temos pistas para encontrar o mesmo.
No final, a solução foi colocar o arquivo do docker em uma camada a cima do projeto.
# Estava assim:
--Pasta/
<br>------pasta/arquivo/projeto-compatilhado.csproj
<br>------pasta/aquivo/projeto.csproj
<br>------pasta/arquivo/docker
<br>
Sendo que meu projeto estava dentro de um cloud run, acreditava que ele conseguiria encontrar e rodar o projeto da forma que precisava.
<br>
No final descobrir que tenho que replicar o projeto dentro do google cloud run usando o processo avançado.<br>
Depois disso preciso editor o arquivo de gatilho para ter o caminho da pasta e com o docker.<br>
Colocar o arquivo do docker nessa parta acima do projeto onde pode pegar todos os projetos compartilhados que estão sendo usados.<br>
# Ficando assim:
--Pasta/
<br>------pasta/docker
<br>------pasta/arquivo/projeto-compatilhado.csproj
<br>------pasta/aquivo/projeto.csproj
<br>
Por fim reimplementar, com isso resolvendo o problema.

# Outras falhas:
Aconteceu de além disso ter que reimplementar o projeto para ter que resolver outros problemas, como por exemplo o de não conseguir subir a aplicação atualizada, apesar de ela subir, algumas parte ficaram bugadas, achei que era aplicação, só que não era isso. <br>
Era de fato o problema de tentar tantas coisas que acabou travando alguma coisa por dentro dos processos. <br>
Logo a solução foi refazer a implementação com o escopo de solução.
<br><br>
Esse artigo vai ser reescrito esse é só um rescunho para não esquecer.<br>
<hr>
Desde já agradeço Angelo Silva.
