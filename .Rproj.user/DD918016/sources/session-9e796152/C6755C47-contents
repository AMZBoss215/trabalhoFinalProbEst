# 1. Carregar pacotes necessários
if(!require(MASS)) install.packages("MASS")
if(!require(ggplot2)) install.packages("ggplot2")
if(!require(readr)) install.packages("readr")
library(MASS)
library(ggplot2)
library(readr)

# 2. Importar os dados da tabela da SprintForge
#dados <- data.frame(
#  Sprint = 1:30,
#  Reprocessos = c(4,2,6,3,5,8,3,4,6,2,5,3,7,4,8,5,3,7,4,6,6,4,5,3,7,4,6,5,3,4)
#)
dados <- read_csv("data/sprints.csv")

# 3. Passo 3 — Estatística Descritiva;
media <- mean(dados$Reprocessos)
variancia <- var(dados$Reprocessos)
desvio_padrao <- sd(dados$Reprocessos)
mediana <- median(dados$Reprocessos)
minimo <- min(dados$Reprocessos)
maximo <- max(dados$Reprocessos)
amplitude <- maximo - minimo
cv <- (desvio_padrao / media) * 100

cat("--- ESTATÍSTICA DESCRITIVA ---\nMédia:", media, "\nVariância:", variancia, 
    "\nDesvio Padrão:", desvio_padrao, "\nMediana:", mediana, "\nCV (%):", cv, "\n\n")

# 4. Passo 5 — Intervalo de Confiança 95% (t-Student, sigma desconhecido)
n <- nrow(dados)
erro_padrao <- desvio_padrao / sqrt(n)
graus_liberdade <- n - 1
t_critico <- qt(0.975, df = graus_liberdade)
ic_inferior <- media - (t_critico * erro_padrao)
ic_superior <- media + (t_critico * erro_padrao)

cat("--- INTERVALO DE CONFIANÇA (95%) ---\n[", ic_inferior, ";", ic_superior, "]\n\n")

# 5. Passo 6 — Teste de Hipótese Unilateral à Direita (H0: mu = 3 vs H1: mu > 3)
mu_0 <- 3
t_estatistica <- (media - mu_0) / erro_padrao
p_valor <- pt(t_estatistica, df = graus_liberdade, lower.tail = FALSE)

cat("--- TESTE DE HIPÓTESE ---\nEstatística t:", t_estatistica, "\nValor-p:", p_valor, "\n\n")

# 6. Passo 4 — Ajuste da Binomial Negativa e Probabilidade P(X >= 6)
# Ajuste usando máxima verossimilhança
ajuste_bn <- fitdistr(dados$Reprocessos, "Negative Binomial")
r_estimado <- ajuste_bn$estimate[["size"]]
p_estimado <- r_estimado / (r_estimado + media)

# Cálculo de P(X >= 6) que é 1 - P(X <= 5)
prob_acumulada_5 <- pnbinom(5, size = r_estimado, prob = p_estimado)
prob_X_maior_6 <- 1 - prob_acumulada_5

cat("--- MODELO PROBABILÍSTICO (BN) ---\nParâmetro r (size):", r_estimado, 
    "\nParâmetro p (prob):", p_estimado, "\nP(X >= 6):", prob_X_maior_6, "\n\n")

# 7. Geração do Gráfico Exigido (Histograma + BN + Poisson)
X_vals <- 0:10
dist_poisson <- dpois(X_vals, lambda = media)
dist_bn <- dnbinom(X_vals, size = r_estimado, prob = p_estimado)

df_teorico <- data.frame(
  Reprocessos = rep(X_vals, 2),
  Densidade = c(dist_bn, dist_poisson),
  Modelo = rep(c("Binomial Negativa", "Poisson"), each = length(X_vals))
)

p_plot <- ggplot() +
  geom_histogram(data = dados, aes(x = Reprocessos, y = ..density..), 
                 binwidth = 1, fill = "gray80", color = "black", alpha = 0.6) +
  geom_line(data = df_teorico, aes(x = Reprocessos, y = Densidade, color = Modelo, linetype = Modelo), size = 1) +
  geom_point(data = df_teorico, aes(x = Reprocessos, y = Densidade, color = Modelo)) +
  labs(title = "Reprocessos por Sprint na SprintForge S.A. vs Modelos Teóricos",
       x = "Número de Reprocessos por Sprint",
       y = "Densidade (Proporção)",
       caption = "Fonte: Dados da pesquisa (Equipe 6, 2026).") +
  theme_minimal() +
  scale_color_manual(values = c("orange", "blue"))

# 8. Salvar o gráfico automaticamente na pasta 'plots'
ggsave(
  filename = "plots/grafico_modelos_teoricos.png", 
  plot = p_plot, 
  width = 8, 
  height = 5, 
  dpi = 300
)
