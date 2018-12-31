package com.tasarhane.jsouptweet;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.IOException;

public class MainActivity extends AppCompatActivity {

    private TextView tvYazi;
    private Button btGetir;
    private String url = "https://twitter.com/tasarhane";
    private String tarayici = "Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.86 Safari/537.36";
    private int zamanAsimi = 3 * 1000;
    private String sonTweetMetni;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        tvYazi = (TextView) findViewById(R.id.tv_yazi);
        btGetir = (Button) findViewById(R.id.bt_getir);

        btGetir.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                tweetGetir();
            }
        });
    }

    private void tweetGetir(){

        new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    Document sayfa = Jsoup.connect(url).userAgent(tarayici).timeout(zamanAsimi).get();
                    Element sonTweetSec = sayfa.select("div.js-tweet-text-container").first();
                    sonTweetMetni = sonTweetSec.text();
                } catch (IOException e) {
                    e.printStackTrace();
                    tvYazi.setText("Hata: " + e);
                }
                runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        tvYazi.setText("Son Tweet: " + sonTweetMetni);
                    }
                });
            }
        }).start();
    }
}
