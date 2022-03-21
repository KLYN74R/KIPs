<div align="center">

<span style="color:#F74165">

# Two threads of semver for more flexibility
## THREAD <span style="color:#28E9C3">=></span> KLYNTAR
</span>

</div>

<br><br>

<span style="color:#28E9C3">

# <b>Authors & Metadata</b>

</span>

<b>Date</b>:05.02.2022</br>
<b>Author</b>:Vlad Chernenko</br>
<b>Contacts</b>:[<img src="https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white">](https://t.me/Vlad_Chernenk0)[<img src="https://img.shields.io/badge/ProtonMail-8B89CC?style=for-the-badge&logo=protonmail&logoColor=white">](mailto:vladchernenko@protonmail.com)

</br></br>

<span style="color:#28E9C3">

# <b>Motivation</b>

</span>


Version tracking is very important to keep backward compatibility and bring new features. Due to architecture of Klyntar and symbiotes based on it,we propose to track 2 threads of versioning.

## Threads for the first time

|     Thread ID     |                   General description                        |
|:------------------|:-------------------------------------------------------------|
| <b>CORE_VERSION</b>      | Common versions flow for all the symbiotes for compatibility |
| <b>SYMBIOTE_VERSION</b>  | Symbiote own flow with private features & functions          |