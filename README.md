# DS_Phonepe-Pulse-Data-Visualization-and-Exploration-A-User-Friendly-Tool-Using-Streamlit-and-Plotly
DS_Phonepe Pulse Data Visualization and Exploration: A User-Friendly Tool Using Streamlit and Plotly
import streamlit as st
import pandas as pd
import plotly.express as px

# Load data
@st.cache
def load_data(file_path):
    data = pd.read_csv(file_path)
    return data

# Sidebar
def sidebar():
    st.sidebar.title("DS_Phonepe Pulse Data Visualization")
    file_path = st.sidebar.file_uploader("Upload Data File", type=['csv'])
    return file_path

# Main function
def main():
    st.title("DS_Phonepe Pulse Data Visualization and Exploration")

    # Sidebar
    file_path = sidebar()

    if file_path:
        data = load_data(file_path)

        st.write("## Data Summary")
        st.write(data.head())

        st.write("## Data Visualization")

        # Visualization options
        viz_option = st.selectbox("Select Visualization", ["Line Plot", "Bar Plot"])

        if viz_option == "Line Plot":
            # Line plot
            st.write("### Line Plot")
            fig = px.line(data, x='Date', y='Metric', title='DS_Phonepe Pulse Data Line Plot')
            st.plotly_chart(fig)

        elif viz_option == "Bar Plot":
            # Bar plot
            st.write("### Bar Plot")
            fig = px.bar(data, x='Date', y='Metric', title='DS_Phonepe Pulse Data Bar Plot')
            st.plotly_chart(fig)

if _name_ == "_main_":
    main()
