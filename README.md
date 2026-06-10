# Foodrecommendationsbot
Recommend the food by country
import streamlit as st
import pandas as pd

df = pd.read_csv(r"C:\Users\PRASHANT\OneDrive\Desktop\food.csv")

st.set_page_config(page_title="Food Recommendation Chatbot")


st.title("🍔 Food Recommendation Chatbot")

st.write("Choose your favorite cuisine and food type.")


cuisine = st.selectbox(
    "Select Cuisine",
    sorted(df["C_Type"].dropna().unique())
)

food_type = st.selectbox(
    "Select Type",
    sorted(df["Veg_Non"].dropna().unique())
)


if st.button("Recommend Food"):

    result = df[
        (df["C_Type"] == cuisine) &
        (df["Veg_Non"] == food_type)
    ]

    if not result.empty:
        st.success("Recommended Foods")

        st.dataframe(
            result[["Name", "Describe"]]
        )

    else:
        st.warning("No matching food found.")
