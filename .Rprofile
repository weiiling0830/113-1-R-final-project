library(tidyverse)
install.packages("tidyverse")
library(tidyverse)
# 從遠端 URL 匯入 CSV 檔案 -----
url <- "https://opendata.tycg.gov.tw/api/dataset/f7f45d24-404c-4587-b637-2880b788753e/resource/943ac0ef-164f-4151-8b8b-30357e929421/download"
data <- read_csv(url)
glimpse(data) # 確認資料框的前 3 行
# 計算面積與公告地價的相關係數 -----
# 確保資料框的欄位名稱與欄位資料正確
correlation <- cor(data$面積, data$公告地價, use = "complete.obs")

# 顯示相關係數
correlation
# 視覺化面積與公告地價的相關係數 -----
library(tidyverse)

# 建立散點圖並加上回歸線
ggplot(data, aes(x = 面積, y = 公告地價)) +
  geom_point(color = "blue", alpha = 0.6) + # 散點圖
  geom_smooth(method = "lm", se = FALSE, color = "red", linetype = "dashed") + # 回歸線
  labs(
    title = "面積與公告地價的相關係數趨勢圖",
    subtitle = paste("相關係數: ", round(correlation, 3)),
    x = "面積",
    y = "公告地價"
  ) +
  theme_minimal()
# 從遠端 URL 匯入 CSV 檔案 -----
url <- "https://opendata.tycg.gov.tw/api/dataset/edae14d2-065d-4432-afc0-ee0b845c6132/resource/5d547553-e5d5-4a57-a246-f7d8c54adfef/download"
data <- read_csv(url)
glimpse(data) # 確認資料框的前 3 行
# 計算面積與公告地價的相關係數 -----
# 確保資料框的欄位名稱與欄位資料正確
correlation <- cor(data$面積, data$公告地價, use = "complete.obs")

# 顯示相關係數
correlation
# 匯入新的 CSV 資料並進行分析與視覺化 -----
library(tidyverse)

# 新的 CSV URL
url_new <- "https://opendata.tycg.gov.tw/api/dataset/edae14d2-065d-4432-afc0-ee0b845c6132/resource/5d547553-e5d5-4a57-a246-f7d8c54adfef/download"

# 讀取資料
data_new <- read_csv(url_new)

# 計算面積與公告地價的相關係數
correlation_new <- cor(data_new$面積, data_new$公告地價, use = "complete.obs")

# 繪製趨勢圖
ggplot(data_new, aes(x = 面積, y = 公告地價)) +
  geom_point(color = "blue", alpha = 0.6) + # 散點圖
  geom_smooth(method = "lm", se = FALSE, color = "red", linetype = "dashed") + # 回歸線
  labs(
    title = "面積與公告地價的相關係數趨勢圖",
    subtitle = paste("相關係數: ", round(correlation_new, 3)),
    x = "面積",
    y = "公告地價"
  ) +
  theme_minimal()
# 清理數據並重新繪製圖表 -----
library(tidyverse)

# 過濾掉包含 NA 的行
clean_data <- data_new %>%
  filter(!is.na(面積) & !is.na(公告地價))

# 重新計算相關係數
correlation_clean <- cor(clean_data$面積, clean_data$公告地價, use = "complete.obs")

# 繪製趨勢圖
ggplot(clean_data, aes(x = 面積, y = 公告地價)) +
  geom_point(color = "blue", alpha = 0.6) + # 散點圖
  geom_smooth(method = "lm", se = FALSE, color = "red", linetype = "dashed") + # 回歸線
  labs(
    title = "面積與公告地價的相關係數趨勢圖 (清理後)",
    subtitle = paste("相關係數: ", round(correlation_clean, 3)),
    x = "面積",
    y = "公告地價"
  ) +
  theme_minimal()
# 公告地價平均值長條圖繪製 -----
library(tidyverse)

# 下載兩個資料來源
data1_url <- "https://opendata.tycg.gov.tw/api/dataset/edae14d2-065d-4432-afc0-ee0b845c6132/resource/5d547553-e5d5-4a57-a246-f7d8c54adfef/download"
data2_url <- "https://opendata.tycg.gov.tw/api/dataset/f7f45d24-404c-4587-b637-2880b788753e/resource/943ac0ef-164f-4151-8b8b-30357e929421/download"
"113年度桃園市中壢區土地公告現值及公告地價" <- read_csv(data1_url)
"107年度桃園市中壢區土地公告現值及公告地價" <- read_csv(data2_url)

# 計算每個段小段的平均公告地價
calculate_average <- function(data, source_name) {
  data %>%
    rename_all(tolower) %>%  # 將所有欄位名稱轉為小寫，避免大小寫不匹配問題
    rename(announcement_price = 公告地價, segment = 段小段) %>%  # 確保欄位名稱一致
    mutate(segment = str_extract(segment, "\\d+")) %>%  # 提取段小段中的數字部分
    group_by(segment) %>%
    summarise(average_price = mean(as.numeric(announcement_price), na.rm = TRUE)) %>%
    mutate(source = source_name)
}

# 計算平均公告地價
avg1 <- calculate_average(`113年度桃園市中壢區土地公告現值及公告地價`, "113年度")
avg2 <- calculate_average(`107年度桃園市中壢區土地公告現值及公告地價`, "107年度")

# 合併平均值結果
data_avg <- bind_rows(avg1, avg2)

# 繪製長條圖
data_avg %>%
  ggplot(aes(x = as.factor(segment), y = average_price, fill = source)) +
  geom_bar(stat = "identity", position = "dodge") +
  labs(
    title = "公告地價平均值比較（按段小段）",
    x = "段小段",
    y = "平均公告地價"
  ) +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))
