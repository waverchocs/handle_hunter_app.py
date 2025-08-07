import streamlit as st
import requests
import pandas as pd

st.set_page_config(page_title="Handle Hunter", layout="centered")

st.title("🕵️ Handle Hunter")
st.markdown("Check availability of premium usernames on X (Twitter).")

user_input = st.text_area("Enter usernames (one per line):", height=150)
check_button = st.button("Check Availability")

def check_handle(username):
    url = f"https://x.com/{username}"
    try:
        response = requests.get(url, timeout=5)
        if response.status_code == 404:
            return "✅ Available"
        elif response.status_code == 200:
            return "❌ Taken"
        else:
            return f"❓ Unknown ({response.status_code})"
    except Exception as e:
        return f"⚠️ Error ({str(e)})"

if check_button and user_input:
    usernames = [u.strip() for u in user_input.split("\n") if u.strip()]
    results = [{"Username": u, "Status": check_handle(u)} for u in usernames]
    df = pd.DataFrame(results)
    st.subheader("Results")
    st.dataframe(df)
    csv = df.to_csv(index=False).encode("utf-8")
    st.download_button("📥 Download CSV", data=csv, file_name="handle_results.csv", mime="text/csv")
