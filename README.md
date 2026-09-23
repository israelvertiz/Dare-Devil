using System.Collections;
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.SceneManagement;

public class OpeningSceneController : MonoBehaviour
{
    [Header("UI")]
    public Text storyText;
    public float typeSpeed = 0.04f;
    public float lineDelay = 1.2f;

    [Header("Flow")]
    public string nextSceneName = "MainGame";

    private string[] lines =
    {
        "My name is Jesse.",
        "People in this town are disappearing.",
        "They say a killer is watching us...",
        "They call him Dare Devil.",
        "Tonight, I find out the truth."
    };

    private void Start()
    {
        StartCoroutine(PlayOpening());
    }

    private IEnumerator PlayOpening()
    {
        foreach (string line in lines)
        {
            yield return StartCoroutine(TypeLine(line));
            yield return new WaitForSeconds(lineDelay);
        }

        SceneManager.LoadScene(nextSceneName);
    }

    private IEnumerator TypeLine(string line)
    {
        storyText.text = "";
        foreach (char c in line)
        {
            storyText.text += c;
            yield return new WaitForSeconds(typeSpeed);
        }
    }
}
