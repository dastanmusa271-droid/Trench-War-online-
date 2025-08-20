# Trench-War-online-
1.dünya savaşı mobil oyun 
|
--+--
  |using UnityEngine;

public class WeaponSystem : MonoBehaviour
{
    public GameObject bulletPrefab;
    public Transform firePoint;
    public float fireRate = 0.5f;
    float nextFireTime = 0f;

    void Update()
    {
        if (Input.GetButton("Fire1") && Time.time >= nextFireTime)
        {
            Fire();
            nextFireTime = Time.time + fireRate;
        }
    }

    void Fire()
    {
        Instantiate(bulletPrefab, firePoint.position, firePoint.rotation);
    }
}Time.timeusing UnityEngine;
using UnityEngine.SceneManagement;

public class GameManager : MonoBehaviour
{
    public static GameManager instance;

    public int score = 0;
    public int playerHealth = 100;

    void Awake()
    {
        if (instance == null)
            instance = this;
        else
            Destroy(gameObject);
    }

    public void AddScore(int amount)
    {
        score += amount;
        Debug.Log("Score: " + score);
    }

    public void PlayerHit(int damage)
    {
        playerHealth -= damage;
        if (playerHealth <= 0)
        {
            EndGame();
        }
    }

    void EndGame()
    {
        Debug.Log("Game Over!");
        SceneManager.LoadScene(SceneManager.GetActiveScene().name);
    }
}using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float rotateSpeed = 200f;
    public GameObject bulletPrefab;
    public Transform firePoint;

    void Update()
    {
        // Hareket
        float move = Input.GetAxis("Vertical") * moveSpeed * Time.deltaTime;
        float rotate = Input.GetAxis("Horizontal") * rotateSpeed * Time.deltaTime;
        transform.Translate(0, 0, move);
        transform.Rotate(0, rotate, 0);

        // Ateş
        if (Input.GetKeyDown(KeyCode.Space))
        {
            Shoot();
        }
    }

    void Shoot()
    {
        Instantiate(bulletPrefab, firePoint.position, firePoint.rotation);
    }
}TrenchWarOnline_Lite/
│
├── Assets/
│   ├── Scenes/
│   │   └── Main.unity
│   ├── Scripts/
│   │   ├── PlayerController.cs
│   │   ├── EnemyAI.cs
│   │   ├── GameManager.cs
│   │   └── WeaponSystem.cs
│   ├── Models/
│   │   ├── tank_placeholder.fbx
│   │   ├── plane_placeholder.fbx
│   │   └── soldier_placeholder.fbx
│   ├── Textures/
│   │   ├── tank_texture.png
│   │   ├── plane_texture.png
│   │   └── soldier_texture.png
│   └── UI/
│       ├── HUD.prefab
│       └── crosshair.png
│
├── ProjectSettings/
│   └── ProjectSettings.asset
│
└── Packages/
    └── manifest.jsonMain.unityPlayerController.csEnemyAI.cs
plane_placeholder.fbxmanifest.jsonMain.unityPlayerController.csEnemyAI.csusing UnityEngine;
using UnityEngine.SceneManagement;

public class GameManager : MonoBehaviour
{
    public static GameManager instance;

    public int score = 0;
    public int playerHealth = 100;

    void Awake()
    {
        if (instance == null)
            instance = this;
        else
            Destroy(gameObject);
    }

    public void AddScore(int amount)
    {
        score += amount;
        Debug.Log("Score: " + score);
    }

    public void PlayerHit(int damage)
    {
        playerHealth -= damage;
        if (playerHealth <= 0)
        {
            EndGame();
        }
    }

    void EndGame()
    {
        Debug.Log("Game Over!");
        SceneManager.LoadScene(SceneManager.GetActiveScene().name);
    }
}using UnityEngine;

public class WeaponSystem : MonoBehaviour
{
    public GameObject bulletPrefab;
    public Transform firePoint;
    public float fireRate = 0.5f;
    float nextFireTime = 0f;

    void Update()
    {
        if (Input.GetButton("Fire1") && Time.time >= nextFireTime)
        {
            Fire();
            nextFireTime = Time.time + fireRate;
        }
    }

    void Fire()
    {
        Instantiate(bulletPrefab, firePoint.position, firePoint.rotation);
    }
}|
--+--
  |ProjectSettings.assetmanifest.jsonMain.unityPlayerController.csEnemyAI.cscrosshair.pngHUD.prefabplane_texture.pngsoldier_texture.pngsoldier_placeholder.fbxtank_texture.pngtank_placeholder.fbxplane_placeholder.fbxGameManager.csWeaponSystem.csEnemyAI.csPlayerController.csTime.timeMain.unity# Trench-War-online-
1.dünya savaşı mobil oyun 
|
--+--
  |using UnityEngine;

public class WeaponSystem : MonoBehaviour
{
    public GameObject bulletPrefab;
    public Transform firePoint;
    public float fireRate = 0.5f;
    float nextFireTime = 0f;

    void Update()
    {
        if (Input.GetButton("Fire1") && Time.time >= nextFireTime)
        {
            Fire();
            nextFireTime = Time.time + fireRate;
        }
    }

    void Fire()
    {
        Instantiate(bulletPrefab, firePoint.position, firePoint.rotation);
    }
}Time.timeusing UnityEngine;
using UnityEngine.SceneManagement;

public class GameManager : MonoBehaviour
{
    public static GameManager instance;

    public int score = 0;
    public int playerHealth = 100;

    void Awake()
    {
        if (instance == null)
            instance = this;
        else
            Destroy(gameObject);
    }

    public void AddScore(int amount)
    {
        score += amount;
        Debug.Log("Score: " + score);
    }

    public void PlayerHit(int damage)
    {
        playerHealth -= damage;
        if (playerHealth <= 0)
        {
            EndGame();
        }
    }

    void EndGame()
    {
        Debug.Log("Game Over!");
        SceneManager.LoadScene(SceneManager.GetActiveScene().name);
    }
}using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float rotateSpeed = 200f;
    public GameObject bulletPrefab;
    public Transform firePoint;

    void Update()
    {
        // Hareket
        float move = Input.GetAxis("Vertical") * moveSpeed * Time.deltaTime;
        float rotate = Input.GetAxis("Horizontal") * rotateSpeed * Time.deltaTime;
        transform.Translate(0, 0, move);
        transform.Rotate(0, rotate, 0);

        // Ateş
        if (Input.GetKeyDown(KeyCode.Space))
        {
            Shoot();
        }
    }

    void Shoot()
    {
        Instantiate(bulletPrefab, firePoint.position, firePoint.rotation);
    }
}TrenchWarOnline_Lite/
│
├── Assets/
│   ├── Scenes/
│   │   └── Main.unity
│   ├── Scripts/
│   │   ├── PlayerController.cs
│   │   ├── EnemyAI.cs
│   │   ├── GameManager.cs
│   │   └── WeaponSystem.cs
│   ├── Models/
│   │   ├── tank_placeholder.fbx
│   │   ├── plane_placeholder.fbx
│   │   └── soldier_placeholder.fbx
│   ├── Textures/
│   │   ├── tank_texture.png
│   │   ├── plane_texture.png
│   │   └── soldier_texture.png
│   └── UI/
│       ├── HUD.prefab
│       └── crosshair.png
│
├── ProjectSettings/
│   └── ProjectSettings.asset
│
└── Packages/
    └── manifest.jsonMain.unityPlayerController.csEnemyAI.cs1.dünyaREADME.7z.001
	Tür: 7z / LZMA2:20
	Dosya sayısı: 1
	İçindekilerin boyutu: 2.76KB (2829B)
1