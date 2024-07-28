// ==UserScript==
// @name         Douyin Auto Volume 50% and Unmute
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Tự động mở âm thanh video trên Douyin khi vào trang lần đầu và đặt âm lượng 50%.
// @author       Phan Đức
// @icon         https://private-user-images.githubusercontent.com/120319793/352850943-9aa00857-9f1a-4a3f-b7c8-992cb2161ebb.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MjIxODIyMDEsIm5iZiI6MTcyMjE4MTkwMSwicGF0aCI6Ii8xMjAzMTk3OTMvMzUyODUwOTQzLTlhYTAwODU3LTlmMWEtNGEzZi1iN2M4LTk5MmNiMjE2MWViYi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNzI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDcyOFQxNTUxNDFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lNmFhZmFhYjA4ZDgyMTVmZjkyYzQ3OWU2NmNkMmZhODk0NTViZTcyMzg0NmNhMWYxNWY4YzhkMDkxZTI3YmUyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.AYKXrrps9PPvV6C0Ej31cN2RaKPSPmBOQMVRF9OyW8E
// @match        https://www.douyin.com/*
// @match        https://*.douyin.com/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';

    // Biến lưu trạng thái mute của người dùng
    let userMuted = false;

    // Hàm mở âm thanh và đặt âm lượng nếu người dùng không tắt âm thanh
    function unmuteAndSetVolume(video, volume) {
        if (!userMuted) {
            video.volume = volume;
            video.muted = false;
        }
    }

    // Hàm kiểm tra và thiết lập âm lượng cho tất cả video
    function initializeVideoSettings() {
        let videos = document.querySelectorAll('video');
        videos.forEach(video => {
            // Mở âm thanh và đặt âm lượng khi trang mới tải
            video.muted = false;
            video.volume = 0.5;

            // Lắng nghe sự thay đổi âm thanh để kiểm tra nếu người dùng tắt âm thanh
            video.onvolumechange = () => {
                if (video.muted) {
                    userMuted = true;
                } else {
                    userMuted = false;
                }
            };
        });
    }

    // Chạy hàm thiết lập ngay khi trang tải
    window.addEventListener('load', initializeVideoSettings);

})();
