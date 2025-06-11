using UnityEngine;
using UnityEngine.UI;
using TMPro;

public class WalkerController : MonoBehaviour
{
    [Header("Personagem")]
    public Sprite[] walkSprites;
    private SpriteRenderer spriteRenderer;

    [Header("UI")]
    public Button walkButton;
    public Button speedUpButton;
    public Button autoWalkButton;
    public TextMeshProUGUI distanceText;

    [Header("Configurações de Movimento")]
    public float stepDistance = 0.75f;
    public float speedMultiplier = 1f;
    public float autoWalkInterval = 0.2f;

    private int currentSpriteIndex = 0;
    private float totalDistance = 0f;
    private bool isAutoWalking = false;
    private float autoWalkTimer = 0f;

    void Start()
    {
        spriteRenderer = GetComponent<SpriteRenderer>();
        if (spriteRenderer == null)
            Debug.LogError("WalkerController: Nenhum SpriteRenderer encontrado no GameObject!");

        if (walkButton != null)
            walkButton.onClick.AddListener(Step);

        if (speedUpButton != null)
            speedUpButton.onClick.AddListener(IncreaseSpeed);

        if (autoWalkButton != null)
            autoWalkButton.onClick.AddListener(ToggleAutoWalk);

        UpdateDistanceUI();
    }

    void Update()
    {
        if (isAutoWalking)
        {
            autoWalkTimer += Time.deltaTime;
            if (autoWalkTimer >= autoWalkInterval)
            {
                Step();
                autoWalkTimer = 0f;
            }
        }
    }

    void Step()
    {
        currentSpriteIndex = (currentSpriteIndex + 1) % walkSprites.Length;
        spriteRenderer.sprite = walkSprites[currentSpriteIndex];

        totalDistance += stepDistance * speedMultiplier;
        UpdateDistanceUI();
    }


    void IncreaseSpeed()
    {
        speedMultiplier += 0.5f;
    }

    void ToggleAutoWalk()
    {
        isAutoWalking = !isAutoWalking;
    }

    void UpdateDistanceUI()
    {
        if (distanceText != null)
            distanceText.text = $"Distância: {totalDistance:F2} metros";
    }
}
