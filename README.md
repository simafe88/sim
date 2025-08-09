# sim
just testing  # Install & load packages
packages <- c("httr", "jsonlite", "ggplot2", "dplyr")
lapply(packages, function(p) if (!require(p, character.only = TRUE)) install.packages(p))

library(httr); library(jsonlite); library(ggplot2); library(dplyr)

# Weather function
get_weather <- function(city) {
  key <- Sys.getenv("OPENWEATHER_API_KEY")
  if (key == "") stop("Set OPENWEATHER_API_KEY in .Renviron")
  
  res <- GET("http://api.openweathermap.org/data/2.5/weather",
             query = list(q = city, appid = key, units = "metric", lang = "en"))
  if (status_code(res) == 200) {
    d <- fromJSON(content(res, "text"))
    cat(sprintf("Weather in %s: %.1f°C, %s\n", city, d$main$temp, d$weather[[1]]$description))
  } else cat("City not found or error.\n")
}

# Sample medical data
set.seed(1)
data <- data.frame(
  Age = round(rnor

