using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.Advertisements;
using UnityEngine.SceneManagement;

public class ADSManager : MonoBehaviour {

	/// <summary>
	/// This script causes advertisements to appear.
	/// by jerry
	/// </summary>

#if UNITY_ANDROID
	private string gameId = "1614061";
#endif

    public Button buttonNo;
	public Button buttonYes;

    public string placementId = "rewardedVideo";

    void Start (){    
		if (buttonNo) buttonNo.onClick.AddListener(ShowAdQuit);
		if (buttonYes) buttonYes.onClick.AddListener(ShowAd);

        if (Advertisement.isSupported) {
            Advertisement.Initialize (gameId, true);
        }
				
        if (Advertisement.isSupported) {
            Advertisement.Initialize (gameId, true);
        }
    }

    void Update (){
		if (buttonNo) buttonNo.interactable = Advertisement.IsReady(placementId);
    }

    void ShowAd (){
        ShowOptions options = new ShowOptions();
        options.resultCallback = HandleShowResult;

        Advertisement.Show(placementId, options);
    }

	void ShowAdQuit (){
		ShowOptions options = new ShowOptions ();
		options.resultCallback = HandleShowQuitResult;

		Advertisement.Show (placementId, options);
	}

    void HandleShowResult (ShowResult result){
        if(result == ShowResult.Finished) {
        Debug.Log("Video completed - the player respawned.");
			SceneManager.LoadScene ("Main");

        }else if(result == ShowResult.Skipped) {
			Debug.LogError("Video was skipped - the player died");


        }else if(result == ShowResult.Failed) {
            Debug.LogError("Video failed to show - try again");
			ShowAd ();
        }
    }
	void HandleShowQuitResult (ShowResult result){
		if(result == ShowResult.Finished) {
			Application.Quit ();
			Debug.Log("Video completed - the game has been stopped.");
		}else{
			Debug.LogError("Video failed to show - try again");
			ShowAdQuit ();
		}
	}
}
