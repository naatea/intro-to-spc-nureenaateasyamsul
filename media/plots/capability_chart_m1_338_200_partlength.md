# Filter the data for Machine 1, Pressure = 200, Temperature = 338
data_m1_338_200 <- subset(X024, Machine == 1 & Pressure == 200 & Temperature == 338)

# Define LSL, USL, and Target for PartLength
LSL_partlength <- 48
USL_partlength <- 52
TARGET_partlength <- 50

if (nrow(data_m1_338_200) == 0) {
  plot_title <- "Process Capability: No data for Machine 1, 338K/200kPa"
  p <- ggplotly(ggplot() +
                  labs(title = plot_title,
                       x = expression(\"Part Length (mm)\"),
                       y = "Density") +
                  theme_minimal() +
                  theme(plot.title = element_text(size = 18, hjust = 0.5),
                        axis.title.x = element_text(size = 18),
                        axis.title.y = element_text(size = 18),
                        axis.text = element_text(size = 14),
                        panel.background = element_rect(fill = "white", colour = "white")))
} else {
  plot_title <- "Process Capability for PartLength (Machine 1, 338K/200kPa)"
  p <- ggplotly(ggplot(data_m1_338_200, aes(x = PartLength)) +
                  geom_histogram(aes(y = ..density..), binwidth = 0.5, fill = "#0072B2", color = "white") +
                  geom_density(color = "#D55E00", size = 1) +
                  geom_vline(xintercept = LSL_partlength, linetype = "dashed", color = "darkgreen") +
                  geom_vline(xintercept = USL_partlength, linetype = "dashed", color = "darkgreen") +
                  geom_vline(xintercept = TARGET_partlength, linetype = "dashed", color = "purple") +
                  labs(title = plot_title,
                       x = expression(\"Part Length (mm)\"),
                       y = "Density") +
                  theme_minimal() +
                  theme(plot.title = element_text(size = 18, hjust = 0.5),
                        axis.title.x = element_text(size = 18),
                        axis.title.y = element_text(size = 18),
                        axis.text = element_text(size = 14),
                        panel.background = element_rect(fill = "white", colour = "white")))
}

htmlwidgets::saveWidget(as_widget(p),
                        file = "media/plots/capability_chart_m1_338_200_partlength.html",
                        selfcontained = TRUE)

