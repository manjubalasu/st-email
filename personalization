import openai
#from dotenv import load_dotenv
import os
import streamlit as st

# Load API key from .env file
load_dotenv()
openai.api_key = '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'

# Create a Streamlit application
st.title("Personalized Email OutReach")

# Use text_area for inputting resume and job description
resume = st.text_area("Paste the candidate's resume here:", height=200)
job_description = st.text_area("Paste the job description here:", height=200)

# Add sliders for Skills, culture fit and excitement on the company's mission
skills_match = st.slider("Emphasis on skills Match (1-10):", 1, 10)
culture_fit = st.slider("Emphasis on Culture Fit (1-10):", 1, 10)
excitement_on_mission = st.slider("Excitement on Company's Product or Mission (1-10):", 1, 10)

# Button to trigger comparison
if st.button('Evaluate Match and Generate Invite'):

    # Compare resume and job description
    chat_prompts = [
        [
            {"role": "system", "content": f"You are a hiring manager. Craft a personalized email such that the overall emphasis in the email for skills match should {skills_match}/10, culture_fit should be {culture_fit}/10 and excitement_on_mission should be {excitement_on_mission}/10, your task is to invite a candidate to apply for a job and tell them about their {culture_fit}, {excitement_on_mission}, their skills (identify a few skills) on their resume matches the job. The invite must be short, crisp & succinct with less than 8 sentences as well as personalized."},
            {"role": "user", "content": f"The candidate's resume:\n{resume}"},
            {"role": "user", "content": f"The job description:\n{job_description}"}
        ],
        [
            {"role": "system", "content": f"You are a hiring manager. Craft a personalized email such that the overall emphasi in the email for skills match should {skills_match}/10, culture_fit should be {culture_fit}/10 and excitement_on_mission should be {excitement_on_mission}/10, your task is to invite a candidate to apply for a job and emphasize the unique qualities they possess. Mention how their skills (identify a few skills) on their resume make them a perfect fit for the job. Keep the invite brief and personalized."},
            {"role": "user", "content": f"The candidate's resume:\n{resume}"},
            {"role": "user", "content": f"The job description:\n{job_description}"}
        ]
    ]

    responses = []
    for chat_prompt in chat_prompts:
        response = openai.ChatCompletion.create(
            model="gpt-4",
            messages=chat_prompt,
            max_tokens=2500,
            n=1
        )
        responses.append(response)

    invites = [response['choices'][0]['message']['content'] for response in responses]
    
    # Display generated invites
    for i, invite in enumerate(invites):
        st.write(f"Invite-{i+1}:")
        st.write(invite)
        st.write("---")
