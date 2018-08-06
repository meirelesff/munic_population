# ---
# BANCO POPULACAO (CENSO + ESTIMATIVAS) DO IBGE
# ---


# Pacotes
library(tidyverse)
library(rio)


# Carrega os dados
censo <- import("tabela200.xlsx") %>%
  select(-2) %>%
  setNames(c("cod_ibge", "2000", "2010")) %>%
  mutate_all(as.numeric) %>%
  mutate(cod_ibge = as.character(cod_ibge))


pop <- import("tabela6579.xlsx") %>%
  select(-2) %>%
  mutate_all(as.numeric) %>%
  mutate(cod_ibge = as.character(cod_ibge))


# Une as duas bases
pop_ibge <- censo %>%
  left_join(pop) %>%
  gather("ano", "pop", -cod_ibge) %>%
  arrange(cod_ibge, ano) %>%
  setNames(c("cod_ibge", "year", "population"))


# Salva
save(pop_ibge, file = "pop_ibge_2000_2017.Rda")



ggplot(pop_ibge, aes(x = ano, y = pop, group = cod_ibge)) + geom_line(alpha = 0.2)






