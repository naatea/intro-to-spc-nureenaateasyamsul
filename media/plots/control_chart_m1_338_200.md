
df_filtered <- X024 %>% filter(Machine == 1, Temperature == 338, Pressure == 200)
chart_obj <- qcc(df_filtered$PartLength, type = 'xbar.one')

