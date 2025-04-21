# Gorilla_VMP_Data_Analysis

1. 复习R，常用的数据处理的函数：https://emljames.github.io/GorillaR/index.html
   • read.csv() to read in the data.
	• filter() to keep one row per trial, containing the participant response.
	• select() to keep the relevant columns.
	• set_names() or rename() to name the columns in a more intuitive way.
	• group_by() and summarise() to calculate summary statistics for each participant. These are also useful when producing descriptive statistics across the whole sample
	• mutate() to create new variables based on the content of other columns. We also combined this with ifelse() to create variables based on certain conditions.
	• left_join() and full_join() to join dataframes together horizontally (on the basis of matching row IDs).
	• bind_rows() to “stack” dataframes on top of each other, adding extra rows (on the basis of matching columns).
   • pivot_wider() and pivot_longer() to rearrange data between long and wide formats

2. 合并两个dataframe
   (1) 行合并（bind_rows() or rbind()）:列名必须一致（顺序可以不同，bind_rows() 会自动对齐）;如果列名不一致，bind_rows() 会自动补 NA，但 rbind() 会报错
   df1 <- data.frame(ID = 1:2, score = c(90, 95))
   df2 <- data.frame(ID = 3:4, score = c(85, 88))
   👍df_all <- bind_rows(df1, df2)  # 推荐 tidyverse 方式
   df_all <- rbind(df1, df2) # 或者传统 base R
   
   (2) 列合并（bind_cols() or left_join()）
   如果简单列拼接（行数必须完全一样）
   df1 <- data.frame(ID = 1:2)
   df2 <- data.frame(score = c(90, 95))
   df_merged <- bind_cols(df1, df2)

   如果根据共享变量合并（主键合并，推荐 left_join()）
   df1 <- data.frame(ID = c(1, 2), name = c("Alice", "Bob"))
   df2 <- data.frame(ID = c(1, 2), score = c(90, 95))
   df_joined <- left_join(df1, df2, by = "ID")
   •	👍left_join(): 保留左表所有数据：如果你有一个 gaze 数据表想要按照 Trial ID 对齐行为数据，就会用到 left_join() 这样的操作
	•	right_join(): 保留右表所有数据
	•	inner_join(): 只保留两表都有的
	•	full_join(): 全保留，缺失补 NA


3. here():构建相对路径
   目的：用于构建项目内的相对路径，提升可重复性，避免 hard-coded 文件路径。
   👍怎么使用：要在 RStudio 项目中使用 .Rproj 文件；路径中用逗号分隔每一级文件夹或文件名（而不是用 /）--结合R.project使用特别香，因为自动从 .Rproj 项目根目录开始定位，因此路径不会因电脑或工作路径变动而出错。！
   install.packages("here")
   library(here)
   read_csv(here("data", "L2", "my_file.csv"))
   
   
   
