
df_filtered_resistance <- X024 %>% filter(Machine == 1, Temperature == 338, Pressure == 200)
chart_obj_resistance <- qcc(df_filtered_resistance$PartResistance, type = 'xbar.one')

