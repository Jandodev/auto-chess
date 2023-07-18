<template>
  <div class="newboard">
    <div class="blue merida">
      <div ref="board" class="cg-board-wrap"></div>
    </div>
    <br>
    <button @click="send_gpt_state" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      send_gpt_state
    </button>
    <input v-model="chess_gpt_output" type="text" />
    <br>
    <button @click="clear_board_state_midi" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      clear_board_state_midi
    </button>
    <button @click="send_board_state_midi" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      send_board_state_midi
    </button>
    <button @click="send_midi" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      send_midi
    </button>
    <p>currernt : {{ current_clicked_square}}</p>
    <br>
    <p>last: {{ last_left_square}} Prev: {{ previous_last_left_square }}</p>

    <button @click="load_fischer_random_game" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      load_fischer_random_game
    </button>
    <button @click="test_preformance" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      test_preformance
    </button>
    <div class="pt-4">Scan Targets:</div>
     <span v-for="(target, index) in target_list_piece_moved" class="text-xs font-semibold inline-block py-1 px-2 uppercase rounded text-blueGray-600 bg-blueGray-200 uppercase last:mr-0 mr-1" :key="index">
      {{ target }}
    </span>
    <button @click="sendMessage" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      sendMessage
    </button>
    <p>Toggle Magnet Polarity: {{magnet_state}}</p>
    <button @click="toggle_magnet_polarity" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      toggle_magnet_polarity
    </button>
    <p>MoonRaker Conn ID: {{ moonraker_conn_id }}</p>
    <button @click="query_moonraker_probe" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      query_moonraker_probe
    </button>
    <p>Demo_move</p>
    <button @click="demo_moves(20)" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      demo_move
    </button>
    <p>Probe Response: {{ probe_status }}</p>
    <button @click="draw_square_marker" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      draw_square_marker
    </button>
    <button @click="send_loop" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      Loop Printer
    </button>
    <button @click="turn_on_magnet" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      Turn Mag on
    </button>
    <button @click="turn_off_magnet" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      Turn Mag off
    </button>
    <button @click="draw_smile" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      Draw Smile
    </button>
    <button @click="draw_clear_square" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      Clear Sqaure
    </button>
    <button @click="draw_vector" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      Draw vector
    </button>
    <button @click="draw_logo" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      Draw logo
    </button>
    <button @click="dancing_pawns(10 ,  mag_toggle_time_slider , short_move_time_slider , long_move_time_slider)" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      Dancing pawns
    </button>
    <button @click="home_xy()" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      Home X/Y
    </button>
    <button @click="kings_felleco(50,  mag_toggle_time_slider , short_move_time_slider , long_move_time_slider)" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      kings felleco
    </button>
    <button @click="relative_AN_move( AN_move, mag_toggle_time_slider , short_move_time_slider , long_move_time_slider)" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      Rel_pawn
    </button>
    <input v-model="AN_move" type="text" /> 
    <button @click="recenter_pieces(mag_toggle_time_slider , short_move_time_slider , long_move_time_slider)" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      recenter_pieces
    </button>
    <button @click="relative_pawn_move(mag_toggle_time_slider , short_move_time_slider , long_move_time_slider)" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      relative_pawn_move
    </button>
    <button @click="yeet_piece(yeet_slot , 8000 , 500 , 2300)" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      yeet_piece
    </button>
    <button @click="try_stockfish()" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      try_stockfish
    </button>
    <input v-model="test_capture_pos.color" type="text"/>
    <input v-model="test_capture_pos.flags" type="text"/>
    <input v-model="test_capture_pos.from" type="text"/>
    <input v-model="test_capture_pos.to" type="text"/>
    <input v-model="test_capture_pos.piece" type="text"/>
    <input v-model="test_capture_pos.san" type="text"/>

    <button @click="relative_capture(test_capture_pos)" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      relative_capture
    </button>relative_castle_move
    <button @click="relative_castle_move(test_capture_pos)" class="bg-blueGray-500 text-white active:bg-blueGray-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
      relative_castle_move
    </button>
    <!-- |h4|2746|500|2300 -->
    <input v-model="yeet_slot" type="text" />
    <hr>
    <p>Toggle Moves</p>
    <input type="checkbox" class="" v-model="move_pieces_toggle" />
    <p>ai_move_toggle</p>
    <input type="checkbox" class="" v-model="ai_move_toggle" />
    <p>disable_scanning</p>
    <input type="checkbox" class="" v-model="disable_scanning" />
    <p>magnet_launch_offset</p>
    <VueSlider v-model="magnet_launch_offset" :min="0" :max="20" :tooltip="'always'" :tooltip-placement="'right'" />
    <p> mag_toggle_time_slider </p>
    <VueSlider v-model="mag_toggle_time_slider" :min="0" :max="5000" :tooltip="'always'" :tooltip-placement="'right'" />
    <p> this.short_move_time_slider </p>
    <VueSlider v-model="short_move_time_slider" :min="0" :max="5000" :tooltip="'always'" :tooltip-placement="'right'" />
    <p> this.long_move_time_slider </p>
    <VueSlider v-model="long_move_time_slider" :min="0" :max="5000" :tooltip="'always'" :tooltip-placement="'right'" />
    <div class="pt-4">Scan Targets Filtered:</div>
     <span v-for="(target, index) in scan_targets_filtered" class="text-xs font-semibold inline-block py-1 px-2 uppercase rounded text-blueGray-600 bg-blueGray-200 uppercase last:mr-0 mr-1" :key="index">
      {{ target }}
    </span>
    <div class="pt-4">Scan Targets:</div>
     <span v-for="(target, index) in scan_targets" class="text-xs font-semibold inline-block py-1 px-2 uppercase rounded text-blueGray-600 bg-blueGray-200 uppercase last:mr-0 mr-1" :key="index">
      {{ target }}
    </span>
    <div></div>
    <div>
      <span class="text-xs font-semibold inline-block py-1 px-2 uppercase rounded text-blueGray-600 bg-blueGray-200 uppercase last:mr-0 mr-1">
        {{ this.current_fen }}
    </span>
    </div>
  </div>
</template>

<script type="module">
import { chessboard }  from 'vue-chessboard'
import bus from './bus.js'
import axios from 'axios';

import VueSlider from 'vue-slider-component'

import OpenAI from 'openai-api'

// Uncomment and replace
//const openai = new OpenAI("")

//import {performance, PerformanceObserver} from 'perf_hooks';

// let noteStart = function(noteNum) {
//         //let start = 0;
//         console.log("Started :",noteNum)
//         //createFrequencyOscillator(noteNum, start);

//         // oscillators[noteNum][0].start(start);

//         // // printAudioCtx(false);

//         // oscillators[noteNum][0].onended = function() {
//         //     if (oscillators[noteNum]) {
//         //         oscillators[noteNum][1].disconnect();
//         //         delete oscillators[noteNum];
//         //     }
//         // };
//     }
//     let noteStop = function(noteNum) {
//       console.log("Stopped :", noteNum)
//         // if (oscillators[noteNum]) {
//         //     var eventTime = audioCtx.currentTime;
//         //     var stopTime = eventTime + 0.5;
//         //     oscillators[noteNum][1].gain.setValueAtTime(nodeControls.masterGain.currentValue, eventTime);
//         //     oscillators[noteNum][1].gain.exponentialRampToValueAtTime(0.0001, stopTime);
//         //     oscillators[noteNum][0].stop(stopTime + 0.6);
//         // }
//     }
//     let onMIDISuccess = function(midiAccess) {
//         var midi = midiAccess;  // store in the global (in real usage, would probably keep in an object instance)
//         Array.from(midi.inputs).forEach((input) => {
//             input[1].onmidimessage = MIDIMessageEventHandler;
//         })
//     }
//     let MIDIMessageEventHandler = function(event) {
//         var noteNumber = event.data[1];
//         if (event.data[0] == 144) {
//             if (event.data[2] > 0) {
//                 noteStart(noteNumber, 0.001);
//             } else if (event.data[2] === 0) {
                
//                     noteStop(noteNumber);
//             }
//         } 
//     }
//     let onMIDIFailure = function(msg) {
//         console.error(`Failed to get MIDI access - ${msg}`);
//     }


// if (typeof navigator.requestMIDIAccess !== "undefined") {
//         console.log("Trying to connect")
//         navigator.requestMIDIAccess().then(onMIDISuccess, onMIDIFailure)
//     } else {
//         console.log('MIDI not available');
//     }

export default {
  name: 'newboard',
  extends: chessboard,
  components: {
    VueSlider
  },
  data() {
    return {
      last_trans_cord: 0,
      current_midi_output: "output-3",
      midi_access_obj: [],
      current_clicked_square: 0,
      last_left_square: 0,
      previous_last_left_square: 0,
      print_board: {},
      return_me:'return me',
      current_fen: '',
      scan_targets: {},
      scan_targets_filtered: {},
      slider1: 10,
      mag_toggle_time_slider: 0,
      short_move_time_slider: 0,
      long_move_time_slider: 0,
      AN_move: 'a5',
      yeet_slot: 'h4',
      move_start: '',
      move_end: '',
      move_start_obj: {},
      move_end_obj: {},
      current_move_in_line_vert: 0,
      current_move_in_line_horz: 0,
      current_move_out_line_vert: 0,
      current_move_out_line_horz: 0,
      move_pieces_toggle : false,
      ai_move_toggle: true,
      offset_y_board_length: 10,
      offset_probe_y: 35,
      is_scanning: false,
      check_piece_scanning: false,
      moonraker_conn_id: 0,
      probe_status: '',
      current_scan_square: {},
      target_list_piece_moved: {},
      disable_scanning: true,
      scan_finished: false,
      magnet_state: true,
      magnet_launch_offset: 6,
      chess_gpt_output: "",
      test_capture_pos: {
        "color": "b",
        "from": "d4",
        "to": "e3",
        "flags": "c",
        "piece": "p",
        "captured": "p",
        "san": "dxe3"
      },    
      cord_map: [
        {
          "chess_cord": "a1",
          "real_x": 1,
          "real_y": 1,
          "send_gcode": {
            "gcode": "G1 X0 Y25 F6000",
            "out_val_x": 0,
            "out_val_y": 25
          }
        },
        {
          "chess_cord": "a2",
          "real_x": 1,
          "real_y": 2,
          "send_gcode": {
            "gcode": "G1 X0 Y71.42857142857143 F6000",
            "out_val_x": 0,
            "out_val_y": 71.42857142857143
          }
        },
        {
          "chess_cord": "a3",
          "real_x": 1,
          "real_y": 3,
          "send_gcode": {
            "gcode": "G1 X0 Y117.85714285714286 F6000",
            "out_val_x": 0,
            "out_val_y": 117.85714285714286
          }
        },
        {
          "chess_cord": "a4",
          "real_x": 1,
          "real_y": 4,
          "send_gcode": {
            "gcode": "G1 X0 Y164.28571428571428 F6000",
            "out_val_x": 0,
            "out_val_y": 164.28571428571428
          }
        },
        {
          "chess_cord": "a5",
          "real_x": 1,
          "real_y": 5,
          "send_gcode": {
            "gcode": "G1 X0 Y210.71428571428572 F6000",
            "out_val_x": 0,
            "out_val_y": 210.71428571428572
          }
        },
        {
          "chess_cord": "a6",
          "real_x": 1,
          "real_y": 6,
          "send_gcode": {
            "gcode": "G1 X0 Y257.1428571428571 F6000",
            "out_val_x": 0,
            "out_val_y": 257.1428571428571
          }
        },
        {
          "chess_cord": "a7",
          "real_x": 1,
          "real_y": 7,
          "send_gcode": {
            "gcode": "G1 X0 Y303.57142857142856 F6000",
            "out_val_x": 0,
            "out_val_y": 303.57142857142856
          }
        },
        {
          "chess_cord": "a8",
          "real_x": 1,
          "real_y": 8,
          "send_gcode": {
            "gcode": "G1 X0 Y350 F6000",
            "out_val_x": 0,
            "out_val_y": 350
          }
        },
        {
          "chess_cord": "b1",
          "real_x": 2,
          "real_y": 1,
          "send_gcode": {
            "gcode": "G1 X50 Y25 F6000",
            "out_val_x": 50,
            "out_val_y": 25
          }
        },
        {
          "chess_cord": "b2",
          "real_x": 2,
          "real_y": 2,
          "send_gcode": {
            "gcode": "G1 X50 Y71.42857142857143 F6000",
            "out_val_x": 50,
            "out_val_y": 71.42857142857143
          }
        },
        {
          "chess_cord": "b3",
          "real_x": 2,
          "real_y": 3,
          "send_gcode": {
            "gcode": "G1 X50 Y117.85714285714286 F6000",
            "out_val_x": 50,
            "out_val_y": 117.85714285714286
          }
        },
        {
          "chess_cord": "b4",
          "real_x": 2,
          "real_y": 4,
          "send_gcode": {
            "gcode": "G1 X50 Y164.28571428571428 F6000",
            "out_val_x": 50,
            "out_val_y": 164.28571428571428
          }
        },
        {
          "chess_cord": "b5",
          "real_x": 2,
          "real_y": 5,
          "send_gcode": {
            "gcode": "G1 X50 Y210.71428571428572 F6000",
            "out_val_x": 50,
            "out_val_y": 210.71428571428572
          }
        },
        {
          "chess_cord": "b6",
          "real_x": 2,
          "real_y": 6,
          "send_gcode": {
            "gcode": "G1 X50 Y257.1428571428571 F6000",
            "out_val_x": 50,
            "out_val_y": 257.1428571428571
          }
        },
        {
          "chess_cord": "b7",
          "real_x": 2,
          "real_y": 7,
          "send_gcode": {
            "gcode": "G1 X50 Y303.57142857142856 F6000",
            "out_val_x": 50,
            "out_val_y": 303.57142857142856
          }
        },
        {
          "chess_cord": "b8",
          "real_x": 2,
          "real_y": 8,
          "send_gcode": {
            "gcode": "G1 X50 Y350 F6000",
            "out_val_x": 50,
            "out_val_y": 350
          }
        },
        {
          "chess_cord": "c1",
          "real_x": 3,
          "real_y": 1,
          "send_gcode": {
            "gcode": "G1 X100 Y25 F6000",
            "out_val_x": 100,
            "out_val_y": 25
          }
        },
        {
          "chess_cord": "c2",
          "real_x": 3,
          "real_y": 2,
          "send_gcode": {
            "gcode": "G1 X100 Y71.42857142857143 F6000",
            "out_val_x": 100,
            "out_val_y": 71.42857142857143
          }
        },
        {
          "chess_cord": "c3",
          "real_x": 3,
          "real_y": 3,
          "send_gcode": {
            "gcode": "G1 X100 Y117.85714285714286 F6000",
            "out_val_x": 100,
            "out_val_y": 117.85714285714286
          }
        },
        {
          "chess_cord": "c4",
          "real_x": 3,
          "real_y": 4,
          "send_gcode": {
            "gcode": "G1 X100 Y164.28571428571428 F6000",
            "out_val_x": 100,
            "out_val_y": 164.28571428571428
          }
        },
        {
          "chess_cord": "c5",
          "real_x": 3,
          "real_y": 5,
          "send_gcode": {
            "gcode": "G1 X100 Y210.71428571428572 F6000",
            "out_val_x": 100,
            "out_val_y": 210.71428571428572
          }
        },
        {
          "chess_cord": "c6",
          "real_x": 3,
          "real_y": 6,
          "send_gcode": {
            "gcode": "G1 X100 Y257.1428571428571 F6000",
            "out_val_x": 100,
            "out_val_y": 257.1428571428571
          }
        },
        {
          "chess_cord": "c7",
          "real_x": 3,
          "real_y": 7,
          "send_gcode": {
            "gcode": "G1 X100 Y303.57142857142856 F6000",
            "out_val_x": 100,
            "out_val_y": 303.57142857142856
          }
        },
        {
          "chess_cord": "c8",
          "real_x": 3,
          "real_y": 8,
          "send_gcode": {
            "gcode": "G1 X100 Y350 F6000",
            "out_val_x": 100,
            "out_val_y": 350
          }
        },
        {
          "chess_cord": "d1",
          "real_x": 4,
          "real_y": 1,
          "send_gcode": {
            "gcode": "G1 X150 Y25 F6000",
            "out_val_x": 150,
            "out_val_y": 25
          }
        },
        {
          "chess_cord": "d2",
          "real_x": 4,
          "real_y": 2,
          "send_gcode": {
            "gcode": "G1 X150 Y71.42857142857143 F6000",
            "out_val_x": 150,
            "out_val_y": 71.42857142857143
          }
        },
        {
          "chess_cord": "d3",
          "real_x": 4,
          "real_y": 3,
          "send_gcode": {
            "gcode": "G1 X150 Y117.85714285714286 F6000",
            "out_val_x": 150,
            "out_val_y": 117.85714285714286
          }
        },
        {
          "chess_cord": "d4",
          "real_x": 4,
          "real_y": 4,
          "send_gcode": {
            "gcode": "G1 X150 Y164.28571428571428 F6000",
            "out_val_x": 150,
            "out_val_y": 164.28571428571428
          }
        },
        {
          "chess_cord": "d5",
          "real_x": 4,
          "real_y": 5,
          "send_gcode": {
            "gcode": "G1 X150 Y210.71428571428572 F6000",
            "out_val_x": 150,
            "out_val_y": 210.71428571428572
          }
        },
        {
          "chess_cord": "d6",
          "real_x": 4,
          "real_y": 6,
          "send_gcode": {
            "gcode": "G1 X150 Y257.1428571428571 F6000",
            "out_val_x": 150,
            "out_val_y": 257.1428571428571
          }
        },
        {
          "chess_cord": "d7",
          "real_x": 4,
          "real_y": 7,
          "send_gcode": {
            "gcode": "G1 X150 Y303.57142857142856 F6000",
            "out_val_x": 150,
            "out_val_y": 303.57142857142856
          }
        },
        {
          "chess_cord": "d8",
          "real_x": 4,
          "real_y": 8,
          "send_gcode": {
            "gcode": "G1 X150 Y350 F6000",
            "out_val_x": 150,
            "out_val_y": 350
          }
        },
        {
          "chess_cord": "e1",
          "real_x": 5,
          "real_y": 1,
          "send_gcode": {
            "gcode": "G1 X200 Y25 F6000",
            "out_val_x": 200,
            "out_val_y": 25
          }
        },
        {
          "chess_cord": "e2",
          "real_x": 5,
          "real_y": 2,
          "send_gcode": {
            "gcode": "G1 X200 Y71.42857142857143 F6000",
            "out_val_x": 200,
            "out_val_y": 71.42857142857143
          }
        },
        {
          "chess_cord": "e3",
          "real_x": 5,
          "real_y": 3,
          "send_gcode": {
            "gcode": "G1 X200 Y117.85714285714286 F6000",
            "out_val_x": 200,
            "out_val_y": 117.85714285714286
          }
        },
        {
          "chess_cord": "e4",
          "real_x": 5,
          "real_y": 4,
          "send_gcode": {
            "gcode": "G1 X200 Y164.28571428571428 F6000",
            "out_val_x": 200,
            "out_val_y": 164.28571428571428
          }
        },
        {
          "chess_cord": "e5",
          "real_x": 5,
          "real_y": 5,
          "send_gcode": {
            "gcode": "G1 X200 Y210.71428571428572 F6000",
            "out_val_x": 200,
            "out_val_y": 210.71428571428572
          }
        },
        {
          "chess_cord": "e6",
          "real_x": 5,
          "real_y": 6,
          "send_gcode": {
            "gcode": "G1 X200 Y257.1428571428571 F6000",
            "out_val_x": 200,
            "out_val_y": 257.1428571428571
          }
        },
        {
          "chess_cord": "e7",
          "real_x": 5,
          "real_y": 7,
          "send_gcode": {
            "gcode": "G1 X200 Y303.57142857142856 F6000",
            "out_val_x": 200,
            "out_val_y": 303.57142857142856
          }
        },
        {
          "chess_cord": "e8",
          "real_x": 5,
          "real_y": 8,
          "send_gcode": {
            "gcode": "G1 X200 Y350 F6000",
            "out_val_x": 200,
            "out_val_y": 350
          }
        },
        {
          "chess_cord": "f1",
          "real_x": 6,
          "real_y": 1,
          "send_gcode": {
            "gcode": "G1 X250 Y25 F6000",
            "out_val_x": 250,
            "out_val_y": 25
          }
        },
        {
          "chess_cord": "f2",
          "real_x": 6,
          "real_y": 2,
          "send_gcode": {
            "gcode": "G1 X250 Y71.42857142857143 F6000",
            "out_val_x": 250,
            "out_val_y": 71.42857142857143
          }
        },
        {
          "chess_cord": "f3",
          "real_x": 6,
          "real_y": 3,
          "send_gcode": {
            "gcode": "G1 X250 Y117.85714285714286 F6000",
            "out_val_x": 250,
            "out_val_y": 117.85714285714286
          }
        },
        {
          "chess_cord": "f4",
          "real_x": 6,
          "real_y": 4,
          "send_gcode": {
            "gcode": "G1 X250 Y164.28571428571428 F6000",
            "out_val_x": 250,
            "out_val_y": 164.28571428571428
          }
        },
        {
          "chess_cord": "f5",
          "real_x": 6,
          "real_y": 5,
          "send_gcode": {
            "gcode": "G1 X250 Y210.71428571428572 F6000",
            "out_val_x": 250,
            "out_val_y": 210.71428571428572
          }
        },
        {
          "chess_cord": "f6",
          "real_x": 6,
          "real_y": 6,
          "send_gcode": {
            "gcode": "G1 X250 Y257.1428571428571 F6000",
            "out_val_x": 250,
            "out_val_y": 257.1428571428571
          }
        },
        {
          "chess_cord": "f7",
          "real_x": 6,
          "real_y": 7,
          "send_gcode": {
            "gcode": "G1 X250 Y303.57142857142856 F6000",
            "out_val_x": 250,
            "out_val_y": 303.57142857142856
          }
        },
        {
          "chess_cord": "f8",
          "real_x": 6,
          "real_y": 8,
          "send_gcode": {
            "gcode": "G1 X250 Y350 F6000",
            "out_val_x": 250,
            "out_val_y": 350
          }
        },
        {
          "chess_cord": "g1",
          "real_x": 7,
          "real_y": 1,
          "send_gcode": {
            "gcode": "G1 X300 Y25 F6000",
            "out_val_x": 300,
            "out_val_y": 25
          }
        },
        {
          "chess_cord": "g2",
          "real_x": 7,
          "real_y": 2,
          "send_gcode": {
            "gcode": "G1 X300 Y71.42857142857143 F6000",
            "out_val_x": 300,
            "out_val_y": 71.42857142857143
          }
        },
        {
          "chess_cord": "g3",
          "real_x": 7,
          "real_y": 3,
          "send_gcode": {
            "gcode": "G1 X300 Y117.85714285714286 F6000",
            "out_val_x": 300,
            "out_val_y": 117.85714285714286
          }
        },
        {
          "chess_cord": "g4",
          "real_x": 7,
          "real_y": 4,
          "send_gcode": {
            "gcode": "G1 X300 Y164.28571428571428 F6000",
            "out_val_x": 300,
            "out_val_y": 164.28571428571428
          }
        },
        {
          "chess_cord": "g5",
          "real_x": 7,
          "real_y": 5,
          "send_gcode": {
            "gcode": "G1 X300 Y210.71428571428572 F6000",
            "out_val_x": 300,
            "out_val_y": 210.71428571428572
          }
        },
        {
          "chess_cord": "g6",
          "real_x": 7,
          "real_y": 6,
          "send_gcode": {
            "gcode": "G1 X300 Y257.1428571428571 F6000",
            "out_val_x": 300,
            "out_val_y": 257.1428571428571
          }
        },
        {
          "chess_cord": "g7",
          "real_x": 7,
          "real_y": 7,
          "send_gcode": {
            "gcode": "G1 X300 Y303.57142857142856 F6000",
            "out_val_x": 300,
            "out_val_y": 303.57142857142856
          }
        },
        {
          "chess_cord": "g8",
          "real_x": 7,
          "real_y": 8,
          "send_gcode": {
            "gcode": "G1 X300 Y350 F6000",
            "out_val_x": 300,
            "out_val_y": 350
          }
        },
        {
          "chess_cord": "h1",
          "real_x": 8,
          "real_y": 1,
          "send_gcode": {
            "gcode": "G1 X350 Y25 F6000",
            "out_val_x": 350,
            "out_val_y": 25
          }
        },
        {
          "chess_cord": "h2",
          "real_x": 8,
          "real_y": 2,
          "send_gcode": {
            "gcode": "G1 X350 Y71.42857142857143 F6000",
            "out_val_x": 350,
            "out_val_y": 71.42857142857143
          }
        },
        {
          "chess_cord": "h3",
          "real_x": 8,
          "real_y": 3,
          "send_gcode": {
            "gcode": "G1 X350 Y117.85714285714286 F6000",
            "out_val_x": 350,
            "out_val_y": 117.85714285714286
          }
        },
        {
            "chess_cord": "h4",
            "real_x": 8,
            "real_y": 4,
            "send_gcode": {
              "gcode": "G1 X350 Y164.28571428571428 F6000",
              "out_val_x": 350,
              "out_val_y": 164.28571428571428
            }
          },
        {
          "chess_cord": "h5",
          "real_x": 8,
          "real_y": 5,
          "send_gcode": {
            "gcode": "G1 X350 Y210.71428571428572 F6000",
            "out_val_x": 350,
            "out_val_y": 210.71428571428572
          }
        },
        {
          "chess_cord": "h6",
          "real_x": 8,
          "real_y": 6,
          "send_gcode": {
            "gcode": "G1 X350 Y257.1428571428571 F6000",
            "out_val_x": 350,
            "out_val_y": 257.1428571428571
          }
        },
        {
          "chess_cord": "h7",
          "real_x": 8,
          "real_y": 7,
          "send_gcode": {
            "gcode": "G1 X350 Y303.57142857142856 F6000",
            "out_val_x": 350,
            "out_val_y": 303.57142857142856
          }
        },
        {
          "chess_cord": "h8",
          "real_x": 8,
          "real_y": 8,
          "send_gcode": {
            "gcode": "G1 X350 Y350 F6000",
            "out_val_x": 350,
            "out_val_y": 350
          }
        }
      ],
      // {
      //     "chess_cord": "a1",
      //     "real_x": 1,
      //     "real_y": 1,
      //     "send_gcode": {
      //       "gcode": "G1 X0 Y25 F6000",
      //       "out_val_x": 0,
      //       "out_val_y": 25
      //     }
      //   },
    };
  },
  // watch: {
  //   current_fen() { return this.game.fen() },
  // },
  // computed: {
  //   scan_targets() {
  //     var cur_targets = this.game.moves({verbose: true});
  //     return cur_targets;
  //   }
  // },
  // computed: {
  //   comp_fen() {
  //     return this.game.fen();
  //   },
  // },
  methods: {
    async send_gpt4_state() {
      console.log(JSON.stringify(this.game.moves({ verbose: true })));
      console.log(this.game.fen());
      console.log(this.game.history());
      console.log(this.game.ascii());

      var input_board_state = this.game.fen();
      var input_last_move = JSON.stringify(this.game.history());
      var input_valid_move = JSON.stringify(this.game.moves({ verbose: true }));
      var input_ascii_board = this.game.ascii();

      const chess_gpt_response = await openai.complete({
        engine: "text-davinci-003",
        messages: [
          { role: "system", content: "You are a helpful Chess AI. Provide valid chess moves based on the given data." },
          { role: "user", content: `Input Board State: ${input_board_state}` },
          { role: "user", content: `Input Last Move: ${input_last_move}` },
          { role: "user", content: `Input Valid Moves (choose one of these): ${input_valid_move}` },
          { role: "user", content: `Input Ascii Board:\n${input_ascii_board}` }
        ],
        temperature: 0.5,
        max_tokens: 250,
        top_p: 1,
        frequency_penalty: 0,
        presence_penalty: 0,
        stop: ["user", "system"],
      });

      console.log(chess_gpt_response);

      // Extract the AI's response from the conversation
      const aiResponse = chess_gpt_response.data.choices[0].messages.find(
        (message) => message.role === "assistant"
      );
      
      this.chess_gpt_output = aiResponse ? aiResponse.content : '';

    },
    async send_gpt_state(){
      console.log(JSON.stringify(this.game.moves({verbose : true})))
      console.log(this.game.fen())
      console.log(this.game.history())
      console.log(this.game.ascii())
      var input_board_state = this.game.fen()
      var input_last_move = JSON.stringify(this.game.history())
      var input_valid_move = JSON.stringify(this.game.moves({verbose : true}))
      var input_ascii_board = this.game.ascii()
      const chess_gpt_response = await openai.complete({
        user: 'Jando',
        engine: "text-davinci-003",
        prompt: `###{Chess GPT AI :)}###\nI will send all the required data through the next lines please try to output a valid chess moved based on the information give\nYour goal is to show the world the power of GPT's when given the correct data!\nInput Board State: ${input_board_state}\nInput Last Move: ${input_last_move}\nInput Valid Moves (Choice one of these): ${input_valid_move}\nInput Ascii Board: ${input_ascii_board}\nPlease only respond with one of the moves listed in "Input Valid Moves" :)\n\n####\nChessGPT:`,
        temperature: 0.5,
        max_tokens: 250,
        top_p: 1,
        frequency_penalty: 0,
        presence_penalty: 0,
        stop: ["ChessGPT:"],
        });
        console.log(chess_gpt_response)
        this.chess_gpt_output = chess_gpt_response.data.choices[0].text
      },
    board_update_tick(){
      this.send_board_state_midi();

      //this.send_light_midi([146 , this.last_trans_cord , 50])
      //console.log(this.board)
      //if(this.show_opp_moves)
      this.game.moves({verbose: true}).forEach(move => {
        //console.log(move)
        //this.translate_num_cord_to_an(x1[1] , y1[0])
        var trans_cord = this.translate_cord_map_to_an(move.to).real_y.toString() + this.translate_cord_map_to_an(move.to).real_x.toString()
        //console.log(trans_cord.real_x.toString() + trans_cord.real_y.toString())
        if (move.san.includes("x")){
          this.send_light_midi([144 , trans_cord , 4])
        }else{
          this.send_light_midi([144 , trans_cord , 15])
        }
      });
      this.send_light_midi([146 , this.last_trans_cord , 50])

    },
    clear_board_state_midi(){
      for (let index = 11; index < 88; index++) {
        //const element = array[index];
        this.send_light_midi([144 , index , 0]) 
      }
    },
    send_board_state_midi(){
      //console.log(fen)
      this.clear_board_state_midi()
      this.send_light_midi([146 , 19 , 103])
      //console.log(this.game.fen())
      var current_fen = this.game.fen().split(" ")
      var fen_array = current_fen[0].split('/')
      //var num_skips = 0;
      //console.log(fen_array)
      //console.log(current_fen[0].split(''))
      for (let index = 0; index < fen_array.length; index++) {
        const element = fen_array[index];
        //console.log(fen_array.length - index)
        var current_row = element.split('')
        var offset = false
        var num_offset = 0
        var offset_value = 0
        //console.log(index , "========================================")
        for (let index2 = 0; index2 < current_row.length; index2++) {
          const element2 = current_row[index2];
          //console.log(element2 , "|" , offset, "|",  offset_value  , "|" , index2)
          if (!isNaN(element2 - parseFloat(element2))) {
            //it's a number
            offset = true
            num_offset++
            // if(Number(element2) > 1){
            //   offset_value = (offset_value + Number(element2))
            // }
            offset_value = (offset_value + Number(element2))
            //num_skips = element2
            //index2 = index2 + element2 - 1
            //console.log( index2,"|", element2, "|" , index2 + (element2 - 1))
            //index2 = index2 + (element2 - 1)
            //console.log("Thats a number")
            continue;
          }else{
            if (element2 == element2.toLowerCase())
            {
              // The character is lowercase
              var num_translate_black
              var trans_number_black = (index2 + 1) + (offset_value - num_offset)
              var offset_addition_black = index2 + 1 
              //console.log(trans_number_black , "|" , "black")
              if(offset){
                num_translate_black = (fen_array.length - index).toString() + (trans_number_black).toString()
              }else{
                num_translate_black = (fen_array.length - index).toString() + (offset_addition_black).toString()
              }
              //var num_translate_black = (fen_array.length - index).toString() + (index2 + 1).toString()
              //console.log(element2 , "Lower" , (fen_array.length - index).toString() + (index2 + 1).toString())
              this.send_light_midi([144 , num_translate_black , 103])
              //offset = false
            }
            else
            {
              // The character is uppercase
              var num_translate_white
              var trans_number_white = (index2 + 1) + (offset_value - num_offset)
              var offset_addition_white = index2 + 1 
              //console.log(trans_number_white , "|" , "white")
              if(offset){
                num_translate_white = (fen_array.length - index).toString() + (trans_number_white).toString()
              }else{
                num_translate_white = (fen_array.length - index).toString() + (offset_addition_white).toString()
              }
              //var num_translate_white = (fen_array.length - index).toString() + (index2 + 1).toString()
              //console.log(element2 , "Upper" , (fen_array.length - index).toString() + (index2 + 1).toString())
              this.send_light_midi([144 , num_translate_white , 3])
              //offset = false
            }
          }
          
        }
        
      }
    },
    send_light_midi(location){
      //console.log(location)
      const output = this.midi_access_obj.outputs.get(this.current_midi_output);
      output.send(location)
    },
    send_midi(){
      console.log(this.midi_access_obj)
      const output = this.midi_access_obj.outputs.get(this.current_midi_output);
      console.log(output)
      const noteOnMessage = [[144, 44, 103],[144, 45, 1],[144, 46, 3]];
      //button Options
      //144, 44, 77 on
      //145, 45, 77 flashing
      //146, 46, 77 slow fade
      //output.send(noteOnMessage);
      noteOnMessage.forEach(note => {
        //console.log(note)
        output.send(note)
      });
      //console.log(this.midi_access_obj.MIDIPort)

      // Array.from(this.midi_access_obj.outputs).forEach((output) => {
      //       console.log(output)
      //       //output[1].onmidimessage = this.MIDIMessageEventHandler;
      //   })
  //       function sendMiddleC(midiAccess, portID) {
  //   const noteOnMessage = [0x90, 60, 0x7f];    // note on middle C, full velocity
  //   const output = midiAccess.outputs.get(portID);
  //   output.send(noteOnMessage);  //omitting the timestamp means send immediately.
  //   output.send([0x80, 60, 0x40], window.performance.now() + 1000.0); // timestamp = now + 1000ms.
  // }


    },
    side_row_move_start(noteNum){
      //console.log("Start: " , noteNum);
      this.board_update_tick();
      if(noteNum == 19){
        var fen_color_swap = this.game.fen().split(" ")
        fen_color_swap[1] = "b";
        var fen_color_swapped = fen_color_swap.join(' ');
        //console.log("Swapped fen b: ", fen_color_swapped)
        //this.game.fen('8/8/8/8/8/8/8/8 w - - 0 1')
        this.game.load(fen_color_swapped)
        this.board.set({
          fen: this.game.fen(),
          turnColor: this.toColor(),
          showThreats: true,
          movable: {
            color: this.toColor(),
            dests: this.possibleMoves(),
            events: { after: this.userPlay()},
        }})
        this.send_light_midi([144 , 19 , 3])
      }
      this.board_update_tick();
      //this.send_light_midi([144 , 19 , 3])
    },
    side_row_move_stop(noteNum){
      //console.log("Stopping: " , noteNum);
      var fen_color_swap = this.game.fen().split(" ")
      fen_color_swap[1] = "w";
      var fen_color_swapped = fen_color_swap.join(' ');
      //console.log("Swapped fen w: ", fen_color_swapped)
      //this.game.fen('8/8/8/8/8/8/8/8 w - - 0 1')
      this.game.load(fen_color_swapped)
      this.board.set({
          fen: this.game.fen(),
          turnColor: this.toColor(),
          showThreats: true,
          movable: {
            color: this.toColor(),
            dests: this.possibleMoves(),
            events: { after: this.userPlay()},
        }})
      this.board_update_tick();
      if(noteNum == 89){
        // this.game.clear()
        // this.game.fen('8/8/8/8/8/8/8/8 w - - 0 1')
        // this.board.set({
        //   fen: this.game.fen()
        // })
        this.game.load('rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1')
        this.board.set({
          fen: this.game.fen(),
          turnColor: this.toColor(),
          showThreats: true,
          movable: {
            color: this.toColor(),
            dests: this.possibleMoves(),
            events: { after: this.userPlay()},
          }
        })
        this.last_trans_cord = 0
      }
    },
    noteStart(noteNum) {
        //let start = 0;
        console.log("Started :",noteNum)
        this.current_clicked_square = noteNum
        
        //createFrequencyOscillator(noteNum, start);

        // oscillators[noteNum][0].start(start);

        // // printAudioCtx(false);

        // oscillators[noteNum][0].onended = function() {
        //     if (oscillators[noteNum]) {
        //         oscillators[noteNum][1].disconnect();
        //         delete oscillators[noteNum];
        //     }
        // };
    },
    noteStop(noteNum) {
      this.previous_last_left_square = this.last_left_square
      console.log("Stopped :", noteNum)
      this.last_left_square = noteNum
      //console.log(this.board);
      var last_square = this.previous_last_left_square
      var curr_square = this.last_left_square

      this.board_update_tick();
      this.send_light_midi([146 , this.previous_last_left_square , 45])
      this.send_light_midi([146 , this.last_left_square , 21])

      // var y = this.previous_last_left_square
      // console.log(typeof(x) , [...y+''])
      var x1 = [...last_square+'']
      var y1 = [...last_square+'']
      var x2 = [...curr_square+'']
      var y2 = [...curr_square+'']
      //console.log(x[0] , y[1])
      //console.log(this.previous_last_left_square.slice(0, 0) , this.previous_last_left_square.slice(1, 1))
      var current_an = this.translate_num_cord_to_an(x1[1] , y1[0])
      var current_an_curr = this.translate_num_cord_to_an(x2[1] , y2[0])
      //console.log(current_an.chess_cord);

          let moves = this.game.moves({verbose: true})
          console.log(this.game)
          let threats = []
          var that = this
          //console.log(moves)
          moves.forEach( async function (move) {
            threats.push({orig: current_an.chess_cord, brush: 'blue'})
            threats.push({orig: current_an_curr.chess_cord, brush: 'green'})
            //console.log(current_an.chess_cord , "|", move.chess_cord, "|", current_an_curr.chess_cord,"|" , move)
            //console.log(current_an.chess_cord == move.from);
            //console.log(current_an_curr.chess_cord == move.to);

            if(move.from == current_an_curr.chess_cord){
                console.log("Found Move : ")
                console.log(move)
                var trans_cord = that.translate_cord_map_to_an(move.to).real_y.toString() + that.translate_cord_map_to_an(move.to).real_x.toString()
                //console.log(trans_cord.real_x.toString() + trans_cord.real_y.toString())
                if (move.san.includes("x")){
                  that.send_light_midi([144 , trans_cord , 5])
                }else{
                  that.send_light_midi([144 , trans_cord , 54])
                }
              }

            // for (let index = 0; index < moves.length; index++) {
            //   const find_move = moves[index];
            //   if(find_move.from == current_an_curr.chess_cord){
            //     console.log("Found Move : ")
            //     console.log(find_move)
            //     var trans_cord = that.translate_cord_map_to_an(find_move.to).real_y.toString() + that.translate_cord_map_to_an(find_move.to).real_x.toString()
            //     //console.log(trans_cord.real_x.toString() + trans_cord.real_y.toString())
            //     if (move.san.includes("x")){
            //       that.send_light_midi([144 , trans_cord , 4])
            //     }else{
            //       that.send_light_midi([144 , trans_cord , 54])
            //     }
            //   }
              
            // }

            if(current_an.chess_cord == move.from && current_an_curr.chess_cord == move.to){
              //console.log("both true" , move);
              var piece_moved = that.game.moves({verbose: true}).filter(function(item) {
                return item.from == current_an.chess_cord && item.to == current_an_curr.chess_cord;
                });
                
                console.log(piece_moved[0])

                if(that.move_pieces_toggle){
                  await that.AN_move_router(piece_moved[0]);
                  that.scanned_user_move(move.from , move.to)
                }else{
                  that.scanned_user_move(move.from , move.to)
                }
              
            }
            // if (move['captured']) {
            //   threats.push({orig: move.from, dest: move.to, brush: 'red'})
            // }
            // if (move['san'].includes('+')) {
            //   threats.push({orig: move.from, dest: move.to, brush: 'blue'})
            // }
          })
          this.board.setShapes(threats)
        },

        // if (oscillators[noteNum]) {
        //     var eventTime = audioCtx.currentTime;
        //     var stopTime = eventTime + 0.5;
        //     oscillators[noteNum][1].gain.setValueAtTime(nodeControls.masterGain.currentValue, eventTime);
        //     oscillators[noteNum][1].gain.exponentialRampToValueAtTime(0.0001, stopTime);
        //     oscillators[noteNum][0].stop(stopTime + 0.6);
        // }
    // },
    onMIDISuccess(midiAccess) {
        // when we get a succesful response, run this code
        var midi = midiAccess
        this.midi_access_obj = midiAccess; // this is our raw MIDI data, inputs, outputs, and sysex status
        
        //var that = this;
        //onsole.log(midi)
        //midi.output.send( [144, 63, 73] );
        //const outputs = Array.from(midiAccess.outputs.values());
        //const outputIn = 
        ////console.log(outputs);
        var inputs = midi.inputs.values();
        //outputs[0].send( [0x80, 0x3F, 0x50] );
        //outputs.send([0x80, 0x29, 0x7f]);


        // loop over all available inputs and listen for any MIDI input
        for (var input = inputs.next(); input && !input.done; input = inputs.next()) {
            // each time there is a midi message call the onMIDIMessage function
            //console.log(input)
            input.value.onmidimessage = this.MIDIMessageEventHandler;
            //onMIDIMessage(input.value.onmidimessage , outputs)
        }
        //console.log(midiAccess)
        Array.from(midi.outputs).forEach((output) => {
          //console.log("-=-=-=-=-=-=-=-=")
          // console.log(output)
          // console.log(output[0])
          // console.log(this.current_midi_output)
          // console.log("DSADSAD")
          //console.log(output[1])
          //console.log("-=-=-=-=-=-=-=-=-")
          if(output[1].name === "Launchpad X LPX MIDI In"){ //Launchpad X LPX MIDI In //MIDIOUT2 (LPX MIDI)
            console.log("Setting MIDI Device")
            this.current_midi_output = output[1].id
          }
          //console.log(this.current_midi_output)
        })
        this.board_update_tick()
        this.send_light_midi([146 , 89 , 106])
    },
    // onMIDISuccess(midiAccess) {
    //   this.midi_access_obj = midiAccess
    //   this.board_update_tick()
    //   //console.log(midiAccess)
    //     var midi = midiAccess;  // store in the global (in real usage, would probably keep in an object instance)
    //     Array.from(midi.inputs).forEach((input) => {
    //         console.log(input)
    //         input[1].onmidimessage = this.MIDIMessageEventHandler;
    //     })
    //     Array.from(midi.outputs).forEach((output) => {
    //       console.log(output)
    //       if(output[1].name === "MIDIOUT2 (LPX MIDI)"){
    //         this.current_midi_output = output[1].id
    //       }
    //     })
    // },
    MIDIMessageEventHandler (event) {
        var noteNumber = event.data[1];
        //console.log(event)
        if (event.data[0] == 176) {
            if (event.data[2] > 0) {
                //this.noteStart(noteNumber, 0.001);
                this.side_row_move_start(noteNumber);
            } else if (event.data[2] === 0) {
                
                    this.side_row_move_stop(noteNumber);
            }
        } 
        if (event.data[0] == 144) {
            if (event.data[2] > 0) {
                this.noteStart(noteNumber, 0.001);
            } else if (event.data[2] === 0) {
                
                    this.noteStop(noteNumber);
            }
        } 
    },
    onMIDIFailure(msg) {
        console.error(`Failed to get MIDI access - ${msg}`);
    },
    async load_fischer_random_game(){
      var fs_legal_fen = ["bbqnnrkr/pppppppp/8/8/8/8/PPPPPPPP/BBQNNRKR w KQkq - 0 1","bbqnrnkr/pppppppp/8/8/8/8/PPPPPPPP/BBQNRNKR w KQkq - 0 1","bbqnrknr/pppppppp/8/8/8/8/PPPPPPPP/BBQNRKNR w KQkq - 0 1","bbqnrkrn/pppppppp/8/8/8/8/PPPPPPPP/BBQNRKRN w KQkq - 0 1","bbqrnnkr/pppppppp/8/8/8/8/PPPPPPPP/BBQRNNKR w KQkq - 0 1","bbqrnknr/pppppppp/8/8/8/8/PPPPPPPP/BBQRNKNR w KQkq - 0 1","bbqrnkrn/pppppppp/8/8/8/8/PPPPPPPP/BBQRNKRN w KQkq - 0 1","bbqrknnr/pppppppp/8/8/8/8/PPPPPPPP/BBQRKNNR w KQkq - 0 1","bbqrknrn/pppppppp/8/8/8/8/PPPPPPPP/BBQRKNRN w KQkq - 0 1","bbqrkrnn/pppppppp/8/8/8/8/PPPPPPPP/BBQRKRNN w KQkq - 0 1","bbnqnrkr/pppppppp/8/8/8/8/PPPPPPPP/BBNQNRKR w KQkq - 0 1","bbnqrnkr/pppppppp/8/8/8/8/PPPPPPPP/BBNQRNKR w KQkq - 0 1","bbnqrknr/pppppppp/8/8/8/8/PPPPPPPP/BBNQRKNR w KQkq - 0 1","bbnqrkrn/pppppppp/8/8/8/8/PPPPPPPP/BBNQRKRN w KQkq - 0 1","bbrqnnkr/pppppppp/8/8/8/8/PPPPPPPP/BBRQNNKR w KQkq - 0 1","bbrqnknr/pppppppp/8/8/8/8/PPPPPPPP/BBRQNKNR w KQkq - 0 1","bbrqnkrn/pppppppp/8/8/8/8/PPPPPPPP/BBRQNKRN w KQkq - 0 1","bbrqknnr/pppppppp/8/8/8/8/PPPPPPPP/BBRQKNNR w KQkq - 0 1","bbrqknrn/pppppppp/8/8/8/8/PPPPPPPP/BBRQKNRN w KQkq - 0 1","bbrqkrnn/pppppppp/8/8/8/8/PPPPPPPP/BBRQKRNN w KQkq - 0 1","bbnnqrkr/pppppppp/8/8/8/8/PPPPPPPP/BBNNQRKR w KQkq - 0 1","bbnrqnkr/pppppppp/8/8/8/8/PPPPPPPP/BBNRQNKR w KQkq - 0 1","bbnrqknr/pppppppp/8/8/8/8/PPPPPPPP/BBNRQKNR w KQkq - 0 1","bbnrqkrn/pppppppp/8/8/8/8/PPPPPPPP/BBNRQKRN w KQkq - 0 1","bbrnqnkr/pppppppp/8/8/8/8/PPPPPPPP/BBRNQNKR w KQkq - 0 1","bbrnqknr/pppppppp/8/8/8/8/PPPPPPPP/BBRNQKNR w KQkq - 0 1","bbrnqkrn/pppppppp/8/8/8/8/PPPPPPPP/BBRNQKRN w KQkq - 0 1","bbrkqnnr/pppppppp/8/8/8/8/PPPPPPPP/BBRKQNNR w KQkq - 0 1","bbrkqnrn/pppppppp/8/8/8/8/PPPPPPPP/BBRKQNRN w KQkq - 0 1","bbrkqrnn/pppppppp/8/8/8/8/PPPPPPPP/BBRKQRNN w KQkq - 0 1","bbnnrqkr/pppppppp/8/8/8/8/PPPPPPPP/BBNNRQKR w KQkq - 0 1","bbnrnqkr/pppppppp/8/8/8/8/PPPPPPPP/BBNRNQKR w KQkq - 0 1","bbnrkqnr/pppppppp/8/8/8/8/PPPPPPPP/BBNRKQNR w KQkq - 0 1","bbnrkqrn/pppppppp/8/8/8/8/PPPPPPPP/BBNRKQRN w KQkq - 0 1","bbrnnqkr/pppppppp/8/8/8/8/PPPPPPPP/BBRNNQKR w KQkq - 0 1","bbrnkqnr/pppppppp/8/8/8/8/PPPPPPPP/BBRNKQNR w KQkq - 0 1","bbrnkqrn/pppppppp/8/8/8/8/PPPPPPPP/BBRNKQRN w KQkq - 0 1","bbrknqnr/pppppppp/8/8/8/8/PPPPPPPP/BBRKNQNR w KQkq - 0 1","bbrknqrn/pppppppp/8/8/8/8/PPPPPPPP/BBRKNQRN w KQkq - 0 1","bbrkrqnn/pppppppp/8/8/8/8/PPPPPPPP/BBRKRQNN w KQkq - 0 1","bbnnrkqr/pppppppp/8/8/8/8/PPPPPPPP/BBNNRKQR w KQkq - 0 1","bbnrnkqr/pppppppp/8/8/8/8/PPPPPPPP/BBNRNKQR w KQkq - 0 1","bbnrknqr/pppppppp/8/8/8/8/PPPPPPPP/BBNRKNQR w KQkq - 0 1","bbnrkrqn/pppppppp/8/8/8/8/PPPPPPPP/BBNRKRQN w KQkq - 0 1","bbrnnkqr/pppppppp/8/8/8/8/PPPPPPPP/BBRNNKQR w KQkq - 0 1","bbrnknqr/pppppppp/8/8/8/8/PPPPPPPP/BBRNKNQR w KQkq - 0 1","bbrnkrqn/pppppppp/8/8/8/8/PPPPPPPP/BBRNKRQN w KQkq - 0 1","bbrknnqr/pppppppp/8/8/8/8/PPPPPPPP/BBRKNNQR w KQkq - 0 1","bbrknrqn/pppppppp/8/8/8/8/PPPPPPPP/BBRKNRQN w KQkq - 0 1","bbrkrnqn/pppppppp/8/8/8/8/PPPPPPPP/BBRKRNQN w KQkq - 0 1","bbnnrkrq/pppppppp/8/8/8/8/PPPPPPPP/BBNNRKRQ w KQkq - 0 1","bbnrnkrq/pppppppp/8/8/8/8/PPPPPPPP/BBNRNKRQ w KQkq - 0 1","bbnrknrq/pppppppp/8/8/8/8/PPPPPPPP/BBNRKNRQ w KQkq - 0 1","bbnrkrnq/pppppppp/8/8/8/8/PPPPPPPP/BBNRKRNQ w KQkq - 0 1","bbrnnkrq/pppppppp/8/8/8/8/PPPPPPPP/BBRNNKRQ w KQkq - 0 1","bbrnknrq/pppppppp/8/8/8/8/PPPPPPPP/BBRNKNRQ w KQkq - 0 1","bbrnkrnq/pppppppp/8/8/8/8/PPPPPPPP/BBRNKRNQ w KQkq - 0 1","bbrknnrq/pppppppp/8/8/8/8/PPPPPPPP/BBRKNNRQ w KQkq - 0 1","bbrknrnq/pppppppp/8/8/8/8/PPPPPPPP/BBRKNRNQ w KQkq - 0 1","bbrkrnnq/pppppppp/8/8/8/8/PPPPPPPP/BBRKRNNQ w KQkq - 0 1","bqnbnrkr/pppppppp/8/8/8/8/PPPPPPPP/BQNBNRKR w KQkq - 0 1","bqnbrnkr/pppppppp/8/8/8/8/PPPPPPPP/BQNBRNKR w KQkq - 0 1","bqnbrknr/pppppppp/8/8/8/8/PPPPPPPP/BQNBRKNR w KQkq - 0 1","bqnbrkrn/pppppppp/8/8/8/8/PPPPPPPP/BQNBRKRN w KQkq - 0 1","bqrbnnkr/pppppppp/8/8/8/8/PPPPPPPP/BQRBNNKR w KQkq - 0 1","bqrbnknr/pppppppp/8/8/8/8/PPPPPPPP/BQRBNKNR w KQkq - 0 1","bqrbnkrn/pppppppp/8/8/8/8/PPPPPPPP/BQRBNKRN w KQkq - 0 1","bqrbknnr/pppppppp/8/8/8/8/PPPPPPPP/BQRBKNNR w KQkq - 0 1","bqrbknrn/pppppppp/8/8/8/8/PPPPPPPP/BQRBKNRN w KQkq - 0 1","bqrbkrnn/pppppppp/8/8/8/8/PPPPPPPP/BQRBKRNN w KQkq - 0 1","bnqbnrkr/pppppppp/8/8/8/8/PPPPPPPP/BNQBNRKR w KQkq - 0 1","bnqbrnkr/pppppppp/8/8/8/8/PPPPPPPP/BNQBRNKR w KQkq - 0 1","bnqbrknr/pppppppp/8/8/8/8/PPPPPPPP/BNQBRKNR w KQkq - 0 1","bnqbrkrn/pppppppp/8/8/8/8/PPPPPPPP/BNQBRKRN w KQkq - 0 1","brqbnnkr/pppppppp/8/8/8/8/PPPPPPPP/BRQBNNKR w KQkq - 0 1","brqbnknr/pppppppp/8/8/8/8/PPPPPPPP/BRQBNKNR w KQkq - 0 1","brqbnkrn/pppppppp/8/8/8/8/PPPPPPPP/BRQBNKRN w KQkq - 0 1","brqbknnr/pppppppp/8/8/8/8/PPPPPPPP/BRQBKNNR w KQkq - 0 1","brqbknrn/pppppppp/8/8/8/8/PPPPPPPP/BRQBKNRN w KQkq - 0 1","brqbkrnn/pppppppp/8/8/8/8/PPPPPPPP/BRQBKRNN w KQkq - 0 1","bnnbqrkr/pppppppp/8/8/8/8/PPPPPPPP/BNNBQRKR w KQkq - 0 1","bnrbqnkr/pppppppp/8/8/8/8/PPPPPPPP/BNRBQNKR w KQkq - 0 1","bnrbqknr/pppppppp/8/8/8/8/PPPPPPPP/BNRBQKNR w KQkq - 0 1","bnrbqkrn/pppppppp/8/8/8/8/PPPPPPPP/BNRBQKRN w KQkq - 0 1","brnbqnkr/pppppppp/8/8/8/8/PPPPPPPP/BRNBQNKR w KQkq - 0 1","brnbqknr/pppppppp/8/8/8/8/PPPPPPPP/BRNBQKNR w KQkq - 0 1","brnbqkrn/pppppppp/8/8/8/8/PPPPPPPP/BRNBQKRN w KQkq - 0 1","brkbqnnr/pppppppp/8/8/8/8/PPPPPPPP/BRKBQNNR w KQkq - 0 1","brkbqnrn/pppppppp/8/8/8/8/PPPPPPPP/BRKBQNRN w KQkq - 0 1","brkbqrnn/pppppppp/8/8/8/8/PPPPPPPP/BRKBQRNN w KQkq - 0 1","bnnbrqkr/pppppppp/8/8/8/8/PPPPPPPP/BNNBRQKR w KQkq - 0 1","bnrbnqkr/pppppppp/8/8/8/8/PPPPPPPP/BNRBNQKR w KQkq - 0 1","bnrbkqnr/pppppppp/8/8/8/8/PPPPPPPP/BNRBKQNR w KQkq - 0 1","bnrbkqrn/pppppppp/8/8/8/8/PPPPPPPP/BNRBKQRN w KQkq - 0 1","brnbnqkr/pppppppp/8/8/8/8/PPPPPPPP/BRNBNQKR w KQkq - 0 1","brnbkqnr/pppppppp/8/8/8/8/PPPPPPPP/BRNBKQNR w KQkq - 0 1","brnbkqrn/pppppppp/8/8/8/8/PPPPPPPP/BRNBKQRN w KQkq - 0 1","brkbnqnr/pppppppp/8/8/8/8/PPPPPPPP/BRKBNQNR w KQkq - 0 1","brkbnqrn/pppppppp/8/8/8/8/PPPPPPPP/BRKBNQRN w KQkq - 0 1","brkbrqnn/pppppppp/8/8/8/8/PPPPPPPP/BRKBRQNN w KQkq - 0 1","bnnbrkqr/pppppppp/8/8/8/8/PPPPPPPP/BNNBRKQR w KQkq - 0 1","bnrbnkqr/pppppppp/8/8/8/8/PPPPPPPP/BNRBNKQR w KQkq - 0 1","bnrbknqr/pppppppp/8/8/8/8/PPPPPPPP/BNRBKNQR w KQkq - 0 1","bnrbkrqn/pppppppp/8/8/8/8/PPPPPPPP/BNRBKRQN w KQkq - 0 1","brnbnkqr/pppppppp/8/8/8/8/PPPPPPPP/BRNBNKQR w KQkq - 0 1","brnbknqr/pppppppp/8/8/8/8/PPPPPPPP/BRNBKNQR w KQkq - 0 1","brnbkrqn/pppppppp/8/8/8/8/PPPPPPPP/BRNBKRQN w KQkq - 0 1","brkbnnqr/pppppppp/8/8/8/8/PPPPPPPP/BRKBNNQR w KQkq - 0 1","brkbnrqn/pppppppp/8/8/8/8/PPPPPPPP/BRKBNRQN w KQkq - 0 1","brkbrnqn/pppppppp/8/8/8/8/PPPPPPPP/BRKBRNQN w KQkq - 0 1","bnnbrkrq/pppppppp/8/8/8/8/PPPPPPPP/BNNBRKRQ w KQkq - 0 1","bnrbnkrq/pppppppp/8/8/8/8/PPPPPPPP/BNRBNKRQ w KQkq - 0 1","bnrbknrq/pppppppp/8/8/8/8/PPPPPPPP/BNRBKNRQ w KQkq - 0 1","bnrbkrnq/pppppppp/8/8/8/8/PPPPPPPP/BNRBKRNQ w KQkq - 0 1","brnbnkrq/pppppppp/8/8/8/8/PPPPPPPP/BRNBNKRQ w KQkq - 0 1","brnbknrq/pppppppp/8/8/8/8/PPPPPPPP/BRNBKNRQ w KQkq - 0 1","brnbkrnq/pppppppp/8/8/8/8/PPPPPPPP/BRNBKRNQ w KQkq - 0 1","brkbnnrq/pppppppp/8/8/8/8/PPPPPPPP/BRKBNNRQ w KQkq - 0 1","brkbnrnq/pppppppp/8/8/8/8/PPPPPPPP/BRKBNRNQ w KQkq - 0 1","brkbnrnq/pppppppp/8/8/8/8/PPPPPPPP/BRKBNRNQ w KQkq - 0 1","bqnnrbkr/pppppppp/8/8/8/8/PPPPPPPP/BQNNRBKR w KQkq - 0 1","bqnrnbkr/pppppppp/8/8/8/8/PPPPPPPP/BQNRNBKR w KQkq - 0 1","bqnrkbnr/pppppppp/8/8/8/8/PPPPPPPP/BQNRKBNR w KQkq - 0 1","bqnrkbrn/pppppppp/8/8/8/8/PPPPPPPP/BQNRKBRN w KQkq - 0 1","bqrnnbkr/pppppppp/8/8/8/8/PPPPPPPP/BQRNNBKR w KQkq - 0 1","bqrnkbnr/pppppppp/8/8/8/8/PPPPPPPP/BQRNKBNR w KQkq - 0 1","bqrnkbrn/pppppppp/8/8/8/8/PPPPPPPP/BQRNKBRN w KQkq - 0 1","bqrknbnr/pppppppp/8/8/8/8/PPPPPPPP/BQRKNBNR w KQkq - 0 1","bqrknbrn/pppppppp/8/8/8/8/PPPPPPPP/BQRKNBRN w KQkq - 0 1","bqrkrbnn/pppppppp/8/8/8/8/PPPPPPPP/BQRKRBNN w KQkq - 0 1","bnqnrbkr/pppppppp/8/8/8/8/PPPPPPPP/BNQNRBKR w KQkq - 0 1","bnqrnbkr/pppppppp/8/8/8/8/PPPPPPPP/BNQRNBKR w KQkq - 0 1","bnqrkbnr/pppppppp/8/8/8/8/PPPPPPPP/BNQRKBNR w KQkq - 0 1","bnqrkbrn/pppppppp/8/8/8/8/PPPPPPPP/BNQRKBRN w KQkq - 0 1","brqnnbkr/pppppppp/8/8/8/8/PPPPPPPP/BRQNNBKR w KQkq - 0 1","brqnkbnr/pppppppp/8/8/8/8/PPPPPPPP/BRQNKBNR w KQkq - 0 1","brqnkbrn/pppppppp/8/8/8/8/PPPPPPPP/BRQNKBRN w KQkq - 0 1","brqknbnr/pppppppp/8/8/8/8/PPPPPPPP/BRQKNBNR w KQkq - 0 1","brqknbrn/pppppppp/8/8/8/8/PPPPPPPP/BRQKNBRN w KQkq - 0 1","brqkrbnn/pppppppp/8/8/8/8/PPPPPPPP/BRQKRBNN w KQkq - 0 1","bnnqrbkr/pppppppp/8/8/8/8/PPPPPPPP/BNNQRBKR w KQkq - 0 1","bnrqnbkr/pppppppp/8/8/8/8/PPPPPPPP/BNRQNBKR w KQkq - 0 1","bnrqkbnr/pppppppp/8/8/8/8/PPPPPPPP/BNRQKBNR w KQkq - 0 1","bnrqkbrn/pppppppp/8/8/8/8/PPPPPPPP/BNRQKBRN w KQkq - 0 1","brnqnbkr/pppppppp/8/8/8/8/PPPPPPPP/BRNQNBKR w KQkq - 0 1","brnqkbnr/pppppppp/8/8/8/8/PPPPPPPP/BRNQKBNR w KQkq - 0 1","brnqkbrn/pppppppp/8/8/8/8/PPPPPPPP/BRNQKBRN w KQkq - 0 1","brkqnbnr/pppppppp/8/8/8/8/PPPPPPPP/BRKQNBNR w KQkq - 0 1","brkqnbrn/pppppppp/8/8/8/8/PPPPPPPP/BRKQNBRN w KQkq - 0 1","brkqrbnn/pppppppp/8/8/8/8/PPPPPPPP/BRKQRBNN w KQkq - 0 1","bnnrqbkr/pppppppp/8/8/8/8/PPPPPPPP/BNNRQBKR w KQkq - 0 1","bnrnqbkr/pppppppp/8/8/8/8/PPPPPPPP/BNRNQBKR w KQkq - 0 1","bnrkqbnr/pppppppp/8/8/8/8/PPPPPPPP/BNRKQBNR w KQkq - 0 1","bnrkqbrn/pppppppp/8/8/8/8/PPPPPPPP/BNRKQBRN w KQkq - 0 1","brnnqbkr/pppppppp/8/8/8/8/PPPPPPPP/BRNNQBKR w KQkq - 0 1","brnkqbnr/pppppppp/8/8/8/8/PPPPPPPP/BRNKQBNR w KQkq - 0 1","brnkqbrn/pppppppp/8/8/8/8/PPPPPPPP/BRNKQBRN w KQkq - 0 1","brknqbnr/pppppppp/8/8/8/8/PPPPPPPP/BRKNQBNR w KQkq - 0 1","brknqbrn/pppppppp/8/8/8/8/PPPPPPPP/BRKNQBRN w KQkq - 0 1","brkrqbnn/pppppppp/8/8/8/8/PPPPPPPP/BRKRQBNN w KQkq - 0 1","bnnrkbqr/pppppppp/8/8/8/8/PPPPPPPP/BNNRKBQR w KQkq - 0 1","bnrnkbqr/pppppppp/8/8/8/8/PPPPPPPP/BNRNKBQR w KQkq - 0 1","bnrknbqr/pppppppp/8/8/8/8/PPPPPPPP/BNRKNBQR w KQkq - 0 1","bnrkrbqn/pppppppp/8/8/8/8/PPPPPPPP/BNRKRBQN w KQkq - 0 1","brnnkbqr/pppppppp/8/8/8/8/PPPPPPPP/BRNNKBQR w KQkq - 0 1","brnknbqr/pppppppp/8/8/8/8/PPPPPPPP/BRNKNBQR w KQkq - 0 1","brnkrbqn/pppppppp/8/8/8/8/PPPPPPPP/BRNKRBQN w KQkq - 0 1","brknnbqr/pppppppp/8/8/8/8/PPPPPPPP/BRKNNBQR w KQkq - 0 1","brknrbqn/pppppppp/8/8/8/8/PPPPPPPP/BRKNRBQN w KQkq - 0 1","brkrnbqn/pppppppp/8/8/8/8/PPPPPPPP/BRKRNBQN w KQkq - 0 1","bnnrkbrq/pppppppp/8/8/8/8/PPPPPPPP/BNNRKBRQ w KQkq - 0 1","bnrnkbrq/pppppppp/8/8/8/8/PPPPPPPP/BNRNKBRQ w KQkq - 0 1","bnrknbrq/pppppppp/8/8/8/8/PPPPPPPP/BNRKNBRQ w KQkq - 0 1","bnrkrbnq/pppppppp/8/8/8/8/PPPPPPPP/BNRKRBNQ w KQkq - 0 1","brnnkbrq/pppppppp/8/8/8/8/PPPPPPPP/BRNNKBRQ w KQkq - 0 1","brnknbrq/pppppppp/8/8/8/8/PPPPPPPP/BRNKNBRQ w KQkq - 0 1","brnkrbnq/pppppppp/8/8/8/8/PPPPPPPP/BRNKRBNQ w KQkq - 0 1","brknnbrq/pppppppp/8/8/8/8/PPPPPPPP/BRKNNBRQ w KQkq - 0 1","brknrbnq/pppppppp/8/8/8/8/PPPPPPPP/BRKNRBNQ w KQkq - 0 1","brkrnbnq/pppppppp/8/8/8/8/PPPPPPPP/BRKRNBNQ w KQkq - 0 1","bqnnrkrb/pppppppp/8/8/8/8/PPPPPPPP/BQNNRKRB w KQkq - 0 1","bqnrnkrb/pppppppp/8/8/8/8/PPPPPPPP/BQNRNKRB w KQkq - 0 1","bqnrknrb/pppppppp/8/8/8/8/PPPPPPPP/BQNRKNRB w KQkq - 0 1","bqnrkrnb/pppppppp/8/8/8/8/PPPPPPPP/BQNRKRNB w KQkq - 0 1","bqrnnkrb/pppppppp/8/8/8/8/PPPPPPPP/BQRNNKRB w KQkq - 0 1","bqrnknrb/pppppppp/8/8/8/8/PPPPPPPP/BQRNKNRB w KQkq - 0 1","bqrnkrnb/pppppppp/8/8/8/8/PPPPPPPP/BQRNKRNB w KQkq - 0 1","bqrknnrb/pppppppp/8/8/8/8/PPPPPPPP/BQRKNNRB w KQkq - 0 1","bqrknrnb/pppppppp/8/8/8/8/PPPPPPPP/BQRKNRNB w KQkq - 0 1","bqrkrnnb/pppppppp/8/8/8/8/PPPPPPPP/BQRKRNNB w KQkq - 0 1","bnqnrkrb/pppppppp/8/8/8/8/PPPPPPPP/BNQNRKRB w KQkq - 0 1","bnqrnkrb/pppppppp/8/8/8/8/PPPPPPPP/BNQRNKRB w KQkq - 0 1","bnqrknrb/pppppppp/8/8/8/8/PPPPPPPP/BNQRKNRB w KQkq - 0 1","bnqrkrnb/pppppppp/8/8/8/8/PPPPPPPP/BNQRKRNB w KQkq - 0 1","brqnnkrb/pppppppp/8/8/8/8/PPPPPPPP/BRQNNKRB w KQkq - 0 1","brqnknrb/pppppppp/8/8/8/8/PPPPPPPP/BRQNKNRB w KQkq - 0 1","brqnkrnb/pppppppp/8/8/8/8/PPPPPPPP/BRQNKRNB w KQkq - 0 1","brqknnrb/pppppppp/8/8/8/8/PPPPPPPP/BRQKNNRB w KQkq - 0 1","brqknrnb/pppppppp/8/8/8/8/PPPPPPPP/BRQKNRNB w KQkq - 0 1","brqkrnnb/pppppppp/8/8/8/8/PPPPPPPP/BRQKRNNB w KQkq - 0 1","bnnqrkrb/pppppppp/8/8/8/8/PPPPPPPP/BNNQRKRB w KQkq - 0 1","bnrqnkrb/pppppppp/8/8/8/8/PPPPPPPP/BNRQNKRB w KQkq - 0 1","bnrqknrb/pppppppp/8/8/8/8/PPPPPPPP/BNRQKNRB w KQkq - 0 1","bnrqkrnb/pppppppp/8/8/8/8/PPPPPPPP/BNRQKRNB w KQkq - 0 1","brnqnkrb/pppppppp/8/8/8/8/PPPPPPPP/BRNQNKRB w KQkq - 0 1","brnqknrb/pppppppp/8/8/8/8/PPPPPPPP/BRNQKNRB w KQkq - 0 1","brnqkrnb/pppppppp/8/8/8/8/PPPPPPPP/BRNQKRNB w KQkq - 0 1","brkqnnrb/pppppppp/8/8/8/8/PPPPPPPP/BRKQNNRB w KQkq - 0 1","brkqnrnb/pppppppp/8/8/8/8/PPPPPPPP/BRKQNRNB w KQkq - 0 1","brkqrnnb/pppppppp/8/8/8/8/PPPPPPPP/BRKQRNNB w KQkq - 0 1","bnnrqkrb/pppppppp/8/8/8/8/PPPPPPPP/BNNRQKRB w KQkq - 0 1","bnrnqkrb/pppppppp/8/8/8/8/PPPPPPPP/BNRNQKRB w KQkq - 0 1","bnrkqnrb/pppppppp/8/8/8/8/PPPPPPPP/BNRKQNRB w KQkq - 0 1","bnrkqrnb/pppppppp/8/8/8/8/PPPPPPPP/BNRKQRNB w KQkq - 0 1","brnnqkrb/pppppppp/8/8/8/8/PPPPPPPP/BRNNQKRB w KQkq - 0 1","brnkqnrb/pppppppp/8/8/8/8/PPPPPPPP/BRNKQNRB w KQkq - 0 1","brnkqrnb/pppppppp/8/8/8/8/PPPPPPPP/BRNKQRNB w KQkq - 0 1","brknqnrb/pppppppp/8/8/8/8/PPPPPPPP/BRKNQNRB w KQkq - 0 1","brknqrnb/pppppppp/8/8/8/8/PPPPPPPP/BRKNQRNB w KQkq - 0 1","brkrqnnb/pppppppp/8/8/8/8/PPPPPPPP/BRKRQNNB w KQkq - 0 1","bnnrkqrb/pppppppp/8/8/8/8/PPPPPPPP/BNNRKQRB w KQkq - 0 1","bnrnkqrb/pppppppp/8/8/8/8/PPPPPPPP/BNRNKQRB w KQkq - 0 1","bnrknqrb/pppppppp/8/8/8/8/PPPPPPPP/BNRKNQRB w KQkq - 0 1","bnrkrqnb/pppppppp/8/8/8/8/PPPPPPPP/BNRKRQNB w KQkq - 0 1","brnnkqrb/pppppppp/8/8/8/8/PPPPPPPP/BRNNKQRB w KQkq - 0 1","brnknqrb/pppppppp/8/8/8/8/PPPPPPPP/BRNKNQRB w KQkq - 0 1","brnkrqnb/pppppppp/8/8/8/8/PPPPPPPP/BRNKRQNB w KQkq - 0 1","brknnqrb/pppppppp/8/8/8/8/PPPPPPPP/BRKNNQRB w KQkq - 0 1","brknrqnb/pppppppp/8/8/8/8/PPPPPPPP/BRKNRQNB w KQkq - 0 1","brkrnqnb/pppppppp/8/8/8/8/PPPPPPPP/BRKRNQNB w KQkq - 0 1","bnnrkrqb/pppppppp/8/8/8/8/PPPPPPPP/BNNRKRQB w KQkq - 0 1","bnrnkrqb/pppppppp/8/8/8/8/PPPPPPPP/BNRNKRQB w KQkq - 0 1","bnrknrqb/pppppppp/8/8/8/8/PPPPPPPP/BNRKNRQB w KQkq - 0 1","bnrkrnqb/pppppppp/8/8/8/8/PPPPPPPP/BNRKRNQB w KQkq - 0 1","brnnkrqb/pppppppp/8/8/8/8/PPPPPPPP/BRNNKRQB w KQkq - 0 1","brnknrqb/pppppppp/8/8/8/8/PPPPPPPP/BRNKNRQB w KQkq - 0 1","brnkrnqb/pppppppp/8/8/8/8/PPPPPPPP/BRNKRNQB w KQkq - 0 1","brknnrqb/pppppppp/8/8/8/8/PPPPPPPP/BRKNNRQB w KQkq - 0 1","brknrnqb/pppppppp/8/8/8/8/PPPPPPPP/BRKNRNQB w KQkq - 0 1","brkrnnqb/pppppppp/8/8/8/8/PPPPPPPP/BRKRNNQB w KQkq - 0 1","qbbnnrkr/pppppppp/8/8/8/8/PPPPPPPP/QBBNNRKR w KQkq - 0 1","qbbnrnkr/pppppppp/8/8/8/8/PPPPPPPP/QBBNRNKR w KQkq - 0 1","qbbnrknr/pppppppp/8/8/8/8/PPPPPPPP/QBBNRKNR w KQkq - 0 1","qbbnrkrn/pppppppp/8/8/8/8/PPPPPPPP/QBBNRKRN w KQkq - 0 1","qbbrnnkr/pppppppp/8/8/8/8/PPPPPPPP/QBBRNNKR w KQkq - 0 1","qbbrnknr/pppppppp/8/8/8/8/PPPPPPPP/QBBRNKNR w KQkq - 0 1","qbbrnkrn/pppppppp/8/8/8/8/PPPPPPPP/QBBRNKRN w KQkq - 0 1","qbbrknnr/pppppppp/8/8/8/8/PPPPPPPP/QBBRKNNR w KQkq - 0 1","qbbrknrn/pppppppp/8/8/8/8/PPPPPPPP/QBBRKNRN w KQkq - 0 1","qbbrkrnn/pppppppp/8/8/8/8/PPPPPPPP/QBBRKRNN w KQkq - 0 1","nbbqnrkr/pppppppp/8/8/8/8/PPPPPPPP/NBBQNRKR w KQkq - 0 1","nbbqrnkr/pppppppp/8/8/8/8/PPPPPPPP/NBBQRNKR w KQkq - 0 1","nbbqrknr/pppppppp/8/8/8/8/PPPPPPPP/NBBQRKNR w KQkq - 0 1","nbbqrkrn/pppppppp/8/8/8/8/PPPPPPPP/NBBQRKRN w KQkq - 0 1","rbbqnnkr/pppppppp/8/8/8/8/PPPPPPPP/RBBQNNKR w KQkq - 0 1","rbbqnknr/pppppppp/8/8/8/8/PPPPPPPP/RBBQNKNR w KQkq - 0 1","rbbqnkrn/pppppppp/8/8/8/8/PPPPPPPP/RBBQNKRN w KQkq - 0 1","rbbqknnr/pppppppp/8/8/8/8/PPPPPPPP/RBBQKNNR w KQkq - 0 1","rbbqknrn/pppppppp/8/8/8/8/PPPPPPPP/RBBQKNRN w KQkq - 0 1","rbbqkrnn/pppppppp/8/8/8/8/PPPPPPPP/RBBQKRNN w KQkq - 0 1","nbbnqrkr/pppppppp/8/8/8/8/PPPPPPPP/NBBNQRKR w KQkq - 0 1","nbbrqnkr/pppppppp/8/8/8/8/PPPPPPPP/NBBRQNKR w KQkq - 0 1","nbbrqknr/pppppppp/8/8/8/8/PPPPPPPP/NBBRQKNR w KQkq - 0 1","nbbrqkrn/pppppppp/8/8/8/8/PPPPPPPP/NBBRQKRN w KQkq - 0 1","rbbnqnkr/pppppppp/8/8/8/8/PPPPPPPP/RBBNQNKR w KQkq - 0 1","rbbnqknr/pppppppp/8/8/8/8/PPPPPPPP/RBBNQKNR w KQkq - 0 1","rbbnqkrn/pppppppp/8/8/8/8/PPPPPPPP/RBBNQKRN w KQkq - 0 1","rbbkqnnr/pppppppp/8/8/8/8/PPPPPPPP/RBBKQNNR w KQkq - 0 1","rbbkqnrn/pppppppp/8/8/8/8/PPPPPPPP/RBBKQNRN w KQkq - 0 1","rbbkqrnn/pppppppp/8/8/8/8/PPPPPPPP/RBBKQRNN w KQkq - 0 1","nbbnrqkr/pppppppp/8/8/8/8/PPPPPPPP/NBBNRQKR w KQkq - 0 1","nbbrnqkr/pppppppp/8/8/8/8/PPPPPPPP/NBBRNQKR w KQkq - 0 1","nbbrkqnr/pppppppp/8/8/8/8/PPPPPPPP/NBBRKQNR w KQkq - 0 1","nbbrkqrn/pppppppp/8/8/8/8/PPPPPPPP/NBBRKQRN w KQkq - 0 1","rbbnnqkr/pppppppp/8/8/8/8/PPPPPPPP/RBBNNQKR w KQkq - 0 1","rbbnkqnr/pppppppp/8/8/8/8/PPPPPPPP/RBBNKQNR w KQkq - 0 1","rbbnkqrn/pppppppp/8/8/8/8/PPPPPPPP/RBBNKQRN w KQkq - 0 1","rbbknqnr/pppppppp/8/8/8/8/PPPPPPPP/RBBKNQNR w KQkq - 0 1","rbbknqrn/pppppppp/8/8/8/8/PPPPPPPP/RBBKNQRN w KQkq - 0 1","rbbkrqnn/pppppppp/8/8/8/8/PPPPPPPP/RBBKRQNN w KQkq - 0 1","nbbnrkqr/pppppppp/8/8/8/8/PPPPPPPP/NBBNRKQR w KQkq - 0 1","nbbrnkqr/pppppppp/8/8/8/8/PPPPPPPP/NBBRNKQR w KQkq - 0 1","nbbrknqr/pppppppp/8/8/8/8/PPPPPPPP/NBBRKNQR w KQkq - 0 1","nbbrkrqn/pppppppp/8/8/8/8/PPPPPPPP/NBBRKRQN w KQkq - 0 1","rbbnnkqr/pppppppp/8/8/8/8/PPPPPPPP/RBBNNKQR w KQkq - 0 1","rbbnknqr/pppppppp/8/8/8/8/PPPPPPPP/RBBNKNQR w KQkq - 0 1","rbbnkrqn/pppppppp/8/8/8/8/PPPPPPPP/RBBNKRQN w KQkq - 0 1","rbbknnqr/pppppppp/8/8/8/8/PPPPPPPP/RBBKNNQR w KQkq - 0 1","rbbknrqn/pppppppp/8/8/8/8/PPPPPPPP/RBBKNRQN w KQkq - 0 1","rbbkrnqn/pppppppp/8/8/8/8/PPPPPPPP/RBBKRNQN w KQkq - 0 1","nbbnrkrq/pppppppp/8/8/8/8/PPPPPPPP/NBBNRKRQ w KQkq - 0 1","nbbrnkrq/pppppppp/8/8/8/8/PPPPPPPP/NBBRNKRQ w KQkq - 0 1","nbbrknrq/pppppppp/8/8/8/8/PPPPPPPP/NBBRKNRQ w KQkq - 0 1","nbbrkrnq/pppppppp/8/8/8/8/PPPPPPPP/NBBRKRNQ w KQkq - 0 1","rbbnnkrq/pppppppp/8/8/8/8/PPPPPPPP/RBBNNKRQ w KQkq - 0 1","rbbnknrq/pppppppp/8/8/8/8/PPPPPPPP/RBBNKNRQ w KQkq - 0 1","rbbnkrnq/pppppppp/8/8/8/8/PPPPPPPP/RBBNKRNQ w KQkq - 0 1","rbbknnrq/pppppppp/8/8/8/8/PPPPPPPP/RBBKNNRQ w KQkq - 0 1","rbbknrnq/pppppppp/8/8/8/8/PPPPPPPP/RBBKNRNQ w KQkq - 0 1","rbbkrnnq/pppppppp/8/8/8/8/PPPPPPPP/RBBKRNNQ w KQkq - 0 1","qnbbnrkr/pppppppp/8/8/8/8/PPPPPPPP/QNBBNRKR w KQkq - 0 1","qnbbrnkr/pppppppp/8/8/8/8/PPPPPPPP/QNBBRNKR w KQkq - 0 1","qnbbrknr/pppppppp/8/8/8/8/PPPPPPPP/QNBBRKNR w KQkq - 0 1","qnbbrkrn/pppppppp/8/8/8/8/PPPPPPPP/QNBBRKRN w KQkq - 0 1","qrbbnnkr/pppppppp/8/8/8/8/PPPPPPPP/QRBBNNKR w KQkq - 0 1","qrbbnknr/pppppppp/8/8/8/8/PPPPPPPP/QRBBNKNR w KQkq - 0 1","qrbbnkrn/pppppppp/8/8/8/8/PPPPPPPP/QRBBNKRN w KQkq - 0 1","qrbbknnr/pppppppp/8/8/8/8/PPPPPPPP/QRBBKNNR w KQkq - 0 1","qrbbknrn/pppppppp/8/8/8/8/PPPPPPPP/QRBBKNRN w KQkq - 0 1","qrbbkrnn/pppppppp/8/8/8/8/PPPPPPPP/QRBBKRNN w KQkq - 0 1","nqbbnrkr/pppppppp/8/8/8/8/PPPPPPPP/NQBBNRKR w KQkq - 0 1","nqbbrnkr/pppppppp/8/8/8/8/PPPPPPPP/NQBBRNKR w KQkq - 0 1","nqbbrknr/pppppppp/8/8/8/8/PPPPPPPP/NQBBRKNR w KQkq - 0 1","nqbbrkrn/pppppppp/8/8/8/8/PPPPPPPP/NQBBRKRN w KQkq - 0 1","rqbbnnkr/pppppppp/8/8/8/8/PPPPPPPP/RQBBNNKR w KQkq - 0 1","rqbbnknr/pppppppp/8/8/8/8/PPPPPPPP/RQBBNKNR w KQkq - 0 1","rqbbnkrn/pppppppp/8/8/8/8/PPPPPPPP/RQBBNKRN w KQkq - 0 1","rqbbknnr/pppppppp/8/8/8/8/PPPPPPPP/RQBBKNNR w KQkq - 0 1","rqbbknrn/pppppppp/8/8/8/8/PPPPPPPP/RQBBKNRN w KQkq - 0 1","rqbbkrnn/pppppppp/8/8/8/8/PPPPPPPP/RQBBKRNN w KQkq - 0 1","nnbbqrkr/pppppppp/8/8/8/8/PPPPPPPP/NNBBQRKR w KQkq - 0 1","nrbbqnkr/pppppppp/8/8/8/8/PPPPPPPP/NRBBQNKR w KQkq - 0 1","nrbbqknr/pppppppp/8/8/8/8/PPPPPPPP/NRBBQKNR w KQkq - 0 1","nrbbqkrn/pppppppp/8/8/8/8/PPPPPPPP/NRBBQKRN w KQkq - 0 1","rnbbqnkr/pppppppp/8/8/8/8/PPPPPPPP/RNBBQNKR w KQkq - 0 1","rnbbqknr/pppppppp/8/8/8/8/PPPPPPPP/RNBBQKNR w KQkq - 0 1","rnbbqkrn/pppppppp/8/8/8/8/PPPPPPPP/RNBBQKRN w KQkq - 0 1","rkbbqnnr/pppppppp/8/8/8/8/PPPPPPPP/RKBBQNNR w KQkq - 0 1","rkbbqnrn/pppppppp/8/8/8/8/PPPPPPPP/RKBBQNRN w KQkq - 0 1","rkbbqrnn/pppppppp/8/8/8/8/PPPPPPPP/RKBBQRNN w KQkq - 0 1","nnbbrqkr/pppppppp/8/8/8/8/PPPPPPPP/NNBBRQKR w KQkq - 0 1","nrbbnqkr/pppppppp/8/8/8/8/PPPPPPPP/NRBBNQKR w KQkq - 0 1","nrbbkqnr/pppppppp/8/8/8/8/PPPPPPPP/NRBBKQNR w KQkq - 0 1","nrbbkqrn/pppppppp/8/8/8/8/PPPPPPPP/NRBBKQRN w KQkq - 0 1","rnbbnqkr/pppppppp/8/8/8/8/PPPPPPPP/RNBBNQKR w KQkq - 0 1","rnbbkqnr/pppppppp/8/8/8/8/PPPPPPPP/RNBBKQNR w KQkq - 0 1","rnbbkqrn/pppppppp/8/8/8/8/PPPPPPPP/RNBBKQRN w KQkq - 0 1","rkbbnqnr/pppppppp/8/8/8/8/PPPPPPPP/RKBBNQNR w KQkq - 0 1","rkbbnqrn/pppppppp/8/8/8/8/PPPPPPPP/RKBBNQRN w KQkq - 0 1","rkbbrqnn/pppppppp/8/8/8/8/PPPPPPPP/RKBBRQNN w KQkq - 0 1","nnbbrkqr/pppppppp/8/8/8/8/PPPPPPPP/NNBBRKQR w KQkq - 0 1","nrbbnkqr/pppppppp/8/8/8/8/PPPPPPPP/NRBBNKQR w KQkq - 0 1","nrbbknqr/pppppppp/8/8/8/8/PPPPPPPP/NRBBKNQR w KQkq - 0 1","nrbbkrqn/pppppppp/8/8/8/8/PPPPPPPP/NRBBKRQN w KQkq - 0 1","rnbbnkqr/pppppppp/8/8/8/8/PPPPPPPP/RNBBNKQR w KQkq - 0 1","rnbbknqr/pppppppp/8/8/8/8/PPPPPPPP/RNBBKNQR w KQkq - 0 1","rnbbkrqn/pppppppp/8/8/8/8/PPPPPPPP/RNBBKRQN w KQkq - 0 1","rkbbnnqr/pppppppp/8/8/8/8/PPPPPPPP/RKBBNNQR w KQkq - 0 1","rkbbnrqn/pppppppp/8/8/8/8/PPPPPPPP/RKBBNRQN w KQkq - 0 1","rkbbrnqn/pppppppp/8/8/8/8/PPPPPPPP/RKBBRNQN w KQkq - 0 1","nnbbrkrq/pppppppp/8/8/8/8/PPPPPPPP/NNBBRKRQ w KQkq - 0 1","nrbbnkrq/pppppppp/8/8/8/8/PPPPPPPP/NRBBNKRQ w KQkq - 0 1","nrbbknrq/pppppppp/8/8/8/8/PPPPPPPP/NRBBKNRQ w KQkq - 0 1","nrbbkrnq/pppppppp/8/8/8/8/PPPPPPPP/NRBBKRNQ w KQkq - 0 1","rnbbnkrq/pppppppp/8/8/8/8/PPPPPPPP/RNBBNKRQ w KQkq - 0 1","rnbbknrq/pppppppp/8/8/8/8/PPPPPPPP/RNBBKNRQ w KQkq - 0 1","rnbbkrnq/pppppppp/8/8/8/8/PPPPPPPP/RNBBKRNQ w KQkq - 0 1","rkbbnnrq/pppppppp/8/8/8/8/PPPPPPPP/RKBBNNRQ w KQkq - 0 1","rkbbnrnq/pppppppp/8/8/8/8/PPPPPPPP/RKBBNRNQ w KQkq - 0 1","rkbbrnnq/pppppppp/8/8/8/8/PPPPPPPP/RKBBRNNQ w KQkq - 0 1","qnbnrbkr/pppppppp/8/8/8/8/PPPPPPPP/QNBNRBKR w KQkq - 0 1","qnbrnbkr/pppppppp/8/8/8/8/PPPPPPPP/QNBRNBKR w KQkq - 0 1","qnbrkbnr/pppppppp/8/8/8/8/PPPPPPPP/QNBRKBNR w KQkq - 0 1","qnbrkbrn/pppppppp/8/8/8/8/PPPPPPPP/QNBRKBRN w KQkq - 0 1","qrbnnbkr/pppppppp/8/8/8/8/PPPPPPPP/QRBNNBKR w KQkq - 0 1","qrbnkbnr/pppppppp/8/8/8/8/PPPPPPPP/QRBNKBNR w KQkq - 0 1","qrbnkbrn/pppppppp/8/8/8/8/PPPPPPPP/QRBNKBRN w KQkq - 0 1","qrbknbnr/pppppppp/8/8/8/8/PPPPPPPP/QRBKNBNR w KQkq - 0 1","qrbknbrn/pppppppp/8/8/8/8/PPPPPPPP/QRBKNBRN w KQkq - 0 1","qrbkrbnn/pppppppp/8/8/8/8/PPPPPPPP/QRBKRBNN w KQkq - 0 1","nqbnrbkr/pppppppp/8/8/8/8/PPPPPPPP/NQBNRBKR w KQkq - 0 1","nqbrnbkr/pppppppp/8/8/8/8/PPPPPPPP/NQBRNBKR w KQkq - 0 1","nqbrkbnr/pppppppp/8/8/8/8/PPPPPPPP/NQBRKBNR w KQkq - 0 1","nqbrkbrn/pppppppp/8/8/8/8/PPPPPPPP/NQBRKBRN w KQkq - 0 1","rqbnnbkr/pppppppp/8/8/8/8/PPPPPPPP/RQBNNBKR w KQkq - 0 1","rqbnkbnr/pppppppp/8/8/8/8/PPPPPPPP/RQBNKBNR w KQkq - 0 1","rqbnkbrn/pppppppp/8/8/8/8/PPPPPPPP/RQBNKBRN w KQkq - 0 1","rqbknbnr/pppppppp/8/8/8/8/PPPPPPPP/RQBKNBNR w KQkq - 0 1","rqbknbrn/pppppppp/8/8/8/8/PPPPPPPP/RQBKNBRN w KQkq - 0 1","rqbkrbnn/pppppppp/8/8/8/8/PPPPPPPP/RQBKRBNN w KQkq - 0 1","nnbqrbkr/pppppppp/8/8/8/8/PPPPPPPP/NNBQRBKR w KQkq - 0 1","nrbqnbkr/pppppppp/8/8/8/8/PPPPPPPP/NRBQNBKR w KQkq - 0 1","nrbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/NRBQKBNR w KQkq - 0 1","nrbqkbrn/pppppppp/8/8/8/8/PPPPPPPP/NRBQKBRN w KQkq - 0 1","rnbqnbkr/pppppppp/8/8/8/8/PPPPPPPP/RNBQNBKR w KQkq - 0 1","rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1","rnbqkbrn/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBRN w KQkq - 0 1","rkbqnbnr/pppppppp/8/8/8/8/PPPPPPPP/RKBQNBNR w KQkq - 0 1","rkbqnbrn/pppppppp/8/8/8/8/PPPPPPPP/RKBQNBRN w KQkq - 0 1","rkbqrbnn/pppppppp/8/8/8/8/PPPPPPPP/RKBQRBNN w KQkq - 0 1","nnbrqbkr/pppppppp/8/8/8/8/PPPPPPPP/NNBRQBKR w KQkq - 0 1","nrbnqbkr/pppppppp/8/8/8/8/PPPPPPPP/NRBNQBKR w KQkq - 0 1","nrbkqbnr/pppppppp/8/8/8/8/PPPPPPPP/NRBKQBNR w KQkq - 0 1","nrbkqbrn/pppppppp/8/8/8/8/PPPPPPPP/NRBKQBRN w KQkq - 0 1","rnbnqbkr/pppppppp/8/8/8/8/PPPPPPPP/RNBNQBKR w KQkq - 0 1","rnbkqbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBKQBNR w KQkq - 0 1","rnbkqbrn/pppppppp/8/8/8/8/PPPPPPPP/RNBKQBRN w KQkq - 0 1","rkbnqbnr/pppppppp/8/8/8/8/PPPPPPPP/RKBNQBNR w KQkq - 0 1","rkbnqbrn/pppppppp/8/8/8/8/PPPPPPPP/RKBNQBRN w KQkq - 0 1","rkbrqbnn/pppppppp/8/8/8/8/PPPPPPPP/RKBRQBNN w KQkq - 0 1","nnbrkbqr/pppppppp/8/8/8/8/PPPPPPPP/NNBRKBQR w KQkq - 0 1","nrbnkbqr/pppppppp/8/8/8/8/PPPPPPPP/NRBNKBQR w KQkq - 0 1","nrbknbqr/pppppppp/8/8/8/8/PPPPPPPP/NRBKNBQR w KQkq - 0 1","nrbkrbqn/pppppppp/8/8/8/8/PPPPPPPP/NRBKRBQN w KQkq - 0 1","rnbnkbqr/pppppppp/8/8/8/8/PPPPPPPP/RNBNKBQR w KQkq - 0 1","rnbknbqr/pppppppp/8/8/8/8/PPPPPPPP/RNBKNBQR w KQkq - 0 1","rnbkrbqn/pppppppp/8/8/8/8/PPPPPPPP/RNBKRBQN w KQkq - 0 1","rkbnnbqr/pppppppp/8/8/8/8/PPPPPPPP/RKBNNBQR w KQkq - 0 1","rkbnrbqn/pppppppp/8/8/8/8/PPPPPPPP/RKBNRBQN w KQkq - 0 1","rkbrnbqn/pppppppp/8/8/8/8/PPPPPPPP/RKBRNBQN w KQkq - 0 1","nnbrkbrq/pppppppp/8/8/8/8/PPPPPPPP/NNBRKBRQ w KQkq - 0 1","nrbnkbrq/pppppppp/8/8/8/8/PPPPPPPP/NRBNKBRQ w KQkq - 0 1","nrbknbrq/pppppppp/8/8/8/8/PPPPPPPP/NRBKNBRQ w KQkq - 0 1","nrbkrbnq/pppppppp/8/8/8/8/PPPPPPPP/NRBKRBNQ w KQkq - 0 1","rnbnkbrq/pppppppp/8/8/8/8/PPPPPPPP/RNBNKBRQ w KQkq - 0 1","rnbknbrq/pppppppp/8/8/8/8/PPPPPPPP/RNBKNBRQ w KQkq - 0 1","rnbkrbnq/pppppppp/8/8/8/8/PPPPPPPP/RNBKRBNQ w KQkq - 0 1","rkbnnbrq/pppppppp/8/8/8/8/PPPPPPPP/RKBNNBRQ w KQkq - 0 1","rkbnrbnq/pppppppp/8/8/8/8/PPPPPPPP/RKBNRBNQ w KQkq - 0 1","rkbrnbnq/pppppppp/8/8/8/8/PPPPPPPP/RKBRNBNQ w KQkq - 0 1","qnbnrkrb/pppppppp/8/8/8/8/PPPPPPPP/QNBNRKRB w KQkq - 0 1","qnbrnkrb/pppppppp/8/8/8/8/PPPPPPPP/QNBRNKRB w KQkq - 0 1","qnbrknrb/pppppppp/8/8/8/8/PPPPPPPP/QNBRKNRB w KQkq - 0 1","qnbrkrnb/pppppppp/8/8/8/8/PPPPPPPP/QNBRKRNB w KQkq - 0 1","qrbnnkrb/pppppppp/8/8/8/8/PPPPPPPP/QRBNNKRB w KQkq - 0 1","qrbnknrb/pppppppp/8/8/8/8/PPPPPPPP/QRBNKNRB w KQkq - 0 1","qrbnkrnb/pppppppp/8/8/8/8/PPPPPPPP/QRBNKRNB w KQkq - 0 1","qrbknnrb/pppppppp/8/8/8/8/PPPPPPPP/QRBKNNRB w KQkq - 0 1","qrbknrnb/pppppppp/8/8/8/8/PPPPPPPP/QRBKNRNB w KQkq - 0 1","qrbkrnnb/pppppppp/8/8/8/8/PPPPPPPP/QRBKRNNB w KQkq - 0 1","nqbnrkrb/pppppppp/8/8/8/8/PPPPPPPP/NQBNRKRB w KQkq - 0 1","nqbrnkrb/pppppppp/8/8/8/8/PPPPPPPP/NQBRNKRB w KQkq - 0 1","nqbrknrb/pppppppp/8/8/8/8/PPPPPPPP/NQBRKNRB w KQkq - 0 1","nqbrkrnb/pppppppp/8/8/8/8/PPPPPPPP/NQBRKRNB w KQkq - 0 1","rqbnnkrb/pppppppp/8/8/8/8/PPPPPPPP/RQBNNKRB w KQkq - 0 1","rqbnknrb/pppppppp/8/8/8/8/PPPPPPPP/RQBNKNRB w KQkq - 0 1","rqbnkrnb/pppppppp/8/8/8/8/PPPPPPPP/RQBNKRNB w KQkq - 0 1","rqbknnrb/pppppppp/8/8/8/8/PPPPPPPP/RQBKNNRB w KQkq - 0 1","rqbknrnb/pppppppp/8/8/8/8/PPPPPPPP/RQBKNRNB w KQkq - 0 1","rqbkrnnb/pppppppp/8/8/8/8/PPPPPPPP/RQBKRNNB w KQkq - 0 1","nnbqrkrb/pppppppp/8/8/8/8/PPPPPPPP/NNBQRKRB w KQkq - 0 1","nrbqnkrb/pppppppp/8/8/8/8/PPPPPPPP/NRBQNKRB w KQkq - 0 1","nrbqknrb/pppppppp/8/8/8/8/PPPPPPPP/NRBQKNRB w KQkq - 0 1","nrbqkrnb/pppppppp/8/8/8/8/PPPPPPPP/NRBQKRNB w KQkq - 0 1","rnbqnkrb/pppppppp/8/8/8/8/PPPPPPPP/RNBQNKRB w KQkq - 0 1","rnbqknrb/pppppppp/8/8/8/8/PPPPPPPP/RNBQKNRB w KQkq - 0 1","rnbqkrnb/pppppppp/8/8/8/8/PPPPPPPP/RNBQKRNB w KQkq - 0 1","rkbqnnrb/pppppppp/8/8/8/8/PPPPPPPP/RKBQNNRB w KQkq - 0 1","rkbqnrnb/pppppppp/8/8/8/8/PPPPPPPP/RKBQNRNB w KQkq - 0 1","rkbqrnnb/pppppppp/8/8/8/8/PPPPPPPP/RKBQRNNB w KQkq - 0 1","nnbrqkrb/pppppppp/8/8/8/8/PPPPPPPP/NNBRQKRB w KQkq - 0 1","nrbnqkrb/pppppppp/8/8/8/8/PPPPPPPP/NRBNQKRB w KQkq - 0 1","nrbkqnrb/pppppppp/8/8/8/8/PPPPPPPP/NRBKQNRB w KQkq - 0 1","nrbkqrnb/pppppppp/8/8/8/8/PPPPPPPP/NRBKQRNB w KQkq - 0 1","rnbnqkrb/pppppppp/8/8/8/8/PPPPPPPP/RNBNQKRB w KQkq - 0 1","rnbkqnrb/pppppppp/8/8/8/8/PPPPPPPP/RNBKQNRB w KQkq - 0 1","rnbkqrnb/pppppppp/8/8/8/8/PPPPPPPP/RNBKQRNB w KQkq - 0 1","rkbnqnrb/pppppppp/8/8/8/8/PPPPPPPP/RKBNQNRB w KQkq - 0 1","rkbnqrnb/pppppppp/8/8/8/8/PPPPPPPP/RKBNQRNB w KQkq - 0 1","rkbrqnnb/pppppppp/8/8/8/8/PPPPPPPP/RKBRQNNB w KQkq - 0 1","nnbrkqrb/pppppppp/8/8/8/8/PPPPPPPP/NNBRKQRB w KQkq - 0 1","nrbnkqrb/pppppppp/8/8/8/8/PPPPPPPP/NRBNKQRB w KQkq - 0 1","nrbknqrb/pppppppp/8/8/8/8/PPPPPPPP/NRBKNQRB w KQkq - 0 1","nrbkrqnb/pppppppp/8/8/8/8/PPPPPPPP/NRBKRQNB w KQkq - 0 1","rnbnkqrb/pppppppp/8/8/8/8/PPPPPPPP/RNBNKQRB w KQkq - 0 1","rnbknqrb/pppppppp/8/8/8/8/PPPPPPPP/RNBKNQRB w KQkq - 0 1","rnbkrqnb/pppppppp/8/8/8/8/PPPPPPPP/RNBKRQNB w KQkq - 0 1","rkbnnqrb/pppppppp/8/8/8/8/PPPPPPPP/RKBNNQRB w KQkq - 0 1","rkbnrqnb/pppppppp/8/8/8/8/PPPPPPPP/RKBNRQNB w KQkq - 0 1","rkbrnqnb/pppppppp/8/8/8/8/PPPPPPPP/RKBRNQNB w KQkq - 0 1","nnbrkrqb/pppppppp/8/8/8/8/PPPPPPPP/NNBRKRQB w KQkq - 0 1","nrbnkrqb/pppppppp/8/8/8/8/PPPPPPPP/NRBNKRQB w KQkq - 0 1","nrbknrqb/pppppppp/8/8/8/8/PPPPPPPP/NRBKNRQB w KQkq - 0 1","nrbkrnqb/pppppppp/8/8/8/8/PPPPPPPP/NRBKRNQB w KQkq - 0 1","rnbnkrqb/pppppppp/8/8/8/8/PPPPPPPP/RNBNKRQB w KQkq - 0 1","rnbknrqb/pppppppp/8/8/8/8/PPPPPPPP/RNBKNRQB w KQkq - 0 1","rnbkrnqb/pppppppp/8/8/8/8/PPPPPPPP/RNBKRNQB w KQkq - 0 1","rkbnnrqb/pppppppp/8/8/8/8/PPPPPPPP/RKBNNRQB w KQkq - 0 1","rkbnrnqb/pppppppp/8/8/8/8/PPPPPPPP/RKBNRNQB w KQkq - 0 1","rkbrnnqb/pppppppp/8/8/8/8/PPPPPPPP/RKBRNNQB w KQkq - 0 1","qbnnbrkr/pppppppp/8/8/8/8/PPPPPPPP/QBNNBRKR w KQkq - 0 1","qbnrbnkr/pppppppp/8/8/8/8/PPPPPPPP/QBNRBNKR w KQkq - 0 1","qbnrbknr/pppppppp/8/8/8/8/PPPPPPPP/QBNRBKNR w KQkq - 0 1","qbnrbkrn/pppppppp/8/8/8/8/PPPPPPPP/QBNRBKRN w KQkq - 0 1","qbrnbnkr/pppppppp/8/8/8/8/PPPPPPPP/QBRNBNKR w KQkq - 0 1","qbrnbknr/pppppppp/8/8/8/8/PPPPPPPP/QBRNBKNR w KQkq - 0 1","qbrnbkrn/pppppppp/8/8/8/8/PPPPPPPP/QBRNBKRN w KQkq - 0 1","qbrkbnnr/pppppppp/8/8/8/8/PPPPPPPP/QBRKBNNR w KQkq - 0 1","qbrkbnrn/pppppppp/8/8/8/8/PPPPPPPP/QBRKBNRN w KQkq - 0 1","qbrkbrnn/pppppppp/8/8/8/8/PPPPPPPP/QBRKBRNN w KQkq - 0 1","nbqnbrkr/pppppppp/8/8/8/8/PPPPPPPP/NBQNBRKR w KQkq - 0 1","nbqrbnkr/pppppppp/8/8/8/8/PPPPPPPP/NBQRBNKR w KQkq - 0 1","nbqrbknr/pppppppp/8/8/8/8/PPPPPPPP/NBQRBKNR w KQkq - 0 1","nbqrbkrn/pppppppp/8/8/8/8/PPPPPPPP/NBQRBKRN w KQkq - 0 1","rbqnbnkr/pppppppp/8/8/8/8/PPPPPPPP/RBQNBNKR w KQkq - 0 1","rbqnbknr/pppppppp/8/8/8/8/PPPPPPPP/RBQNBKNR w KQkq - 0 1","rbqnbkrn/pppppppp/8/8/8/8/PPPPPPPP/RBQNBKRN w KQkq - 0 1","rbqkbnnr/pppppppp/8/8/8/8/PPPPPPPP/RBQKBNNR w KQkq - 0 1","rbqkbnrn/pppppppp/8/8/8/8/PPPPPPPP/RBQKBNRN w KQkq - 0 1","rbqkbrnn/pppppppp/8/8/8/8/PPPPPPPP/RBQKBRNN w KQkq - 0 1","nbnqbrkr/pppppppp/8/8/8/8/PPPPPPPP/NBNQBRKR w KQkq - 0 1","nbrqbnkr/pppppppp/8/8/8/8/PPPPPPPP/NBRQBNKR w KQkq - 0 1","nbrqbknr/pppppppp/8/8/8/8/PPPPPPPP/NBRQBKNR w KQkq - 0 1","nbrqbkrn/pppppppp/8/8/8/8/PPPPPPPP/NBRQBKRN w KQkq - 0 1","rbnqbnkr/pppppppp/8/8/8/8/PPPPPPPP/RBNQBNKR w KQkq - 0 1","rbnqbknr/pppppppp/8/8/8/8/PPPPPPPP/RBNQBKNR w KQkq - 0 1","rbnqbkrn/pppppppp/8/8/8/8/PPPPPPPP/RBNQBKRN w KQkq - 0 1","rbkqbnnr/pppppppp/8/8/8/8/PPPPPPPP/RBKQBNNR w KQkq - 0 1","rbkqbnrn/pppppppp/8/8/8/8/PPPPPPPP/RBKQBNRN w KQkq - 0 1","rbkqbrnn/pppppppp/8/8/8/8/PPPPPPPP/RBKQBRNN w KQkq - 0 1","nbnrbqkr/pppppppp/8/8/8/8/PPPPPPPP/NBNRBQKR w KQkq - 0 1","nbrnbqkr/pppppppp/8/8/8/8/PPPPPPPP/NBRNBQKR w KQkq - 0 1","nbrkbqnr/pppppppp/8/8/8/8/PPPPPPPP/NBRKBQNR w KQkq - 0 1","nbrkbqrn/pppppppp/8/8/8/8/PPPPPPPP/NBRKBQRN w KQkq - 0 1","rbnnbqkr/pppppppp/8/8/8/8/PPPPPPPP/RBNNBQKR w KQkq - 0 1","rbnkbqnr/pppppppp/8/8/8/8/PPPPPPPP/RBNKBQNR w KQkq - 0 1","rbnkbqrn/pppppppp/8/8/8/8/PPPPPPPP/RBNKBQRN w KQkq - 0 1","rbknbqnr/pppppppp/8/8/8/8/PPPPPPPP/RBKNBQNR w KQkq - 0 1","rbknbqrn/pppppppp/8/8/8/8/PPPPPPPP/RBKNBQRN w KQkq - 0 1","rbkrbqnn/pppppppp/8/8/8/8/PPPPPPPP/RBKRBQNN w KQkq - 0 1","nbnrbkqr/pppppppp/8/8/8/8/PPPPPPPP/NBNRBKQR w KQkq - 0 1","nbrnbkqr/pppppppp/8/8/8/8/PPPPPPPP/NBRNBKQR w KQkq - 0 1","nbrkbnqr/pppppppp/8/8/8/8/PPPPPPPP/NBRKBNQR w KQkq - 0 1","nbrkbrqn/pppppppp/8/8/8/8/PPPPPPPP/NBRKBRQN w KQkq - 0 1","rbnnbkqr/pppppppp/8/8/8/8/PPPPPPPP/RBNNBKQR w KQkq - 0 1","rbnkbnqr/pppppppp/8/8/8/8/PPPPPPPP/RBNKBNQR w KQkq - 0 1","rbnkbrqn/pppppppp/8/8/8/8/PPPPPPPP/RBNKBRQN w KQkq - 0 1","rbknbnqr/pppppppp/8/8/8/8/PPPPPPPP/RBKNBNQR w KQkq - 0 1","rbknbrqn/pppppppp/8/8/8/8/PPPPPPPP/RBKNBRQN w KQkq - 0 1","rbkrbnqn/pppppppp/8/8/8/8/PPPPPPPP/RBKRBNQN w KQkq - 0 1","nbnrbkrq/pppppppp/8/8/8/8/PPPPPPPP/NBNRBKRQ w KQkq - 0 1","nbrnbkrq/pppppppp/8/8/8/8/PPPPPPPP/NBRNBKRQ w KQkq - 0 1","nbrkbnrq/pppppppp/8/8/8/8/PPPPPPPP/NBRKBNRQ w KQkq - 0 1","nbrkbrnq/pppppppp/8/8/8/8/PPPPPPPP/NBRKBRNQ w KQkq - 0 1","rbnnbkrq/pppppppp/8/8/8/8/PPPPPPPP/RBNNBKRQ w KQkq - 0 1","rbnkbnrq/pppppppp/8/8/8/8/PPPPPPPP/RBNKBNRQ w KQkq - 0 1","rbnkbrnq/pppppppp/8/8/8/8/PPPPPPPP/RBNKBRNQ w KQkq - 0 1","rbknbnrq/pppppppp/8/8/8/8/PPPPPPPP/RBKNBNRQ w KQkq - 0 1","rbknbrnq/pppppppp/8/8/8/8/PPPPPPPP/RBKNBRNQ w KQkq - 0 1","rbkrbnnq/pppppppp/8/8/8/8/PPPPPPPP/RBKRBNNQ w KQkq - 0 1","qnnbbrkr/pppppppp/8/8/8/8/PPPPPPPP/QNNBBRKR w KQkq - 0 1","qnrbbnkr/pppppppp/8/8/8/8/PPPPPPPP/QNRBBNKR w KQkq - 0 1","qnrbbknr/pppppppp/8/8/8/8/PPPPPPPP/QNRBBKNR w KQkq - 0 1","qnrbbkrn/pppppppp/8/8/8/8/PPPPPPPP/QNRBBKRN w KQkq - 0 1","qrnbbnkr/pppppppp/8/8/8/8/PPPPPPPP/QRNBBNKR w KQkq - 0 1","qrnbbknr/pppppppp/8/8/8/8/PPPPPPPP/QRNBBKNR w KQkq - 0 1","qrnbbkrn/pppppppp/8/8/8/8/PPPPPPPP/QRNBBKRN w KQkq - 0 1","qrkbbnnr/pppppppp/8/8/8/8/PPPPPPPP/QRKBBNNR w KQkq - 0 1","qrkbbnrn/pppppppp/8/8/8/8/PPPPPPPP/QRKBBNRN w KQkq - 0 1","qrkbbrnn/pppppppp/8/8/8/8/PPPPPPPP/QRKBBRNN w KQkq - 0 1","nqnbbrkr/pppppppp/8/8/8/8/PPPPPPPP/NQNBBRKR w KQkq - 0 1","nqrbbnkr/pppppppp/8/8/8/8/PPPPPPPP/NQRBBNKR w KQkq - 0 1","nqrbbknr/pppppppp/8/8/8/8/PPPPPPPP/NQRBBKNR w KQkq - 0 1","nqrbbkrn/pppppppp/8/8/8/8/PPPPPPPP/NQRBBKRN w KQkq - 0 1","rqnbbnkr/pppppppp/8/8/8/8/PPPPPPPP/RQNBBNKR w KQkq - 0 1","rqnbbknr/pppppppp/8/8/8/8/PPPPPPPP/RQNBBKNR w KQkq - 0 1","rqnbbkrn/pppppppp/8/8/8/8/PPPPPPPP/RQNBBKRN w KQkq - 0 1","rqkbbnnr/pppppppp/8/8/8/8/PPPPPPPP/RQKBBNNR w KQkq - 0 1","rqkbbnrn/pppppppp/8/8/8/8/PPPPPPPP/RQKBBNRN w KQkq - 0 1","rqkbbrnn/pppppppp/8/8/8/8/PPPPPPPP/RQKBBRNN w KQkq - 0 1","nnqbbrkr/pppppppp/8/8/8/8/PPPPPPPP/NNQBBRKR w KQkq - 0 1","nrqbbnkr/pppppppp/8/8/8/8/PPPPPPPP/NRQBBNKR w KQkq - 0 1","nrqbbknr/pppppppp/8/8/8/8/PPPPPPPP/NRQBBKNR w KQkq - 0 1","nrqbbkrn/pppppppp/8/8/8/8/PPPPPPPP/NRQBBKRN w KQkq - 0 1","rnqbbnkr/pppppppp/8/8/8/8/PPPPPPPP/RNQBBNKR w KQkq - 0 1","rnqbbknr/pppppppp/8/8/8/8/PPPPPPPP/RNQBBKNR w KQkq - 0 1","rnqbbkrn/pppppppp/8/8/8/8/PPPPPPPP/RNQBBKRN w KQkq - 0 1","rkqbbnnr/pppppppp/8/8/8/8/PPPPPPPP/RKQBBNNR w KQkq - 0 1","rkqbbnrn/pppppppp/8/8/8/8/PPPPPPPP/RKQBBNRN w KQkq - 0 1","rkqbbrnn/pppppppp/8/8/8/8/PPPPPPPP/RKQBBRNN w KQkq - 0 1","nnrbbqkr/pppppppp/8/8/8/8/PPPPPPPP/NNRBBQKR w KQkq - 0 1","nrnbbqkr/pppppppp/8/8/8/8/PPPPPPPP/NRNBBQKR w KQkq - 0 1","nrkbbqnr/pppppppp/8/8/8/8/PPPPPPPP/NRKBBQNR w KQkq - 0 1","nrkbbqrn/pppppppp/8/8/8/8/PPPPPPPP/NRKBBQRN w KQkq - 0 1","rnnbbqkr/pppppppp/8/8/8/8/PPPPPPPP/RNNBBQKR w KQkq - 0 1","rnkbbqnr/pppppppp/8/8/8/8/PPPPPPPP/RNKBBQNR w KQkq - 0 1","rnkbbqrn/pppppppp/8/8/8/8/PPPPPPPP/RNKBBQRN w KQkq - 0 1","rknbbqnr/pppppppp/8/8/8/8/PPPPPPPP/RKNBBQNR w KQkq - 0 1","rknbbqrn/pppppppp/8/8/8/8/PPPPPPPP/RKNBBQRN w KQkq - 0 1","rkrbbqnn/pppppppp/8/8/8/8/PPPPPPPP/RKRBBQNN w KQkq - 0 1","nnrbbkqr/pppppppp/8/8/8/8/PPPPPPPP/NNRBBKQR w KQkq - 0 1","nrnbbkqr/pppppppp/8/8/8/8/PPPPPPPP/NRNBBKQR w KQkq - 0 1","nrkbbnqr/pppppppp/8/8/8/8/PPPPPPPP/NRKBBNQR w KQkq - 0 1","nrkbbrqn/pppppppp/8/8/8/8/PPPPPPPP/NRKBBRQN w KQkq - 0 1","rnnbbkqr/pppppppp/8/8/8/8/PPPPPPPP/RNNBBKQR w KQkq - 0 1","rnkbbnqr/pppppppp/8/8/8/8/PPPPPPPP/RNKBBNQR w KQkq - 0 1","rnkbbrqn/pppppppp/8/8/8/8/PPPPPPPP/RNKBBRQN w KQkq - 0 1","rknbbnqr/pppppppp/8/8/8/8/PPPPPPPP/RKNBBNQR w KQkq - 0 1","rknbbrqn/pppppppp/8/8/8/8/PPPPPPPP/RKNBBRQN w KQkq - 0 1","rkrbbnqn/pppppppp/8/8/8/8/PPPPPPPP/RKRBBNQN w KQkq - 0 1","nnrbbkrq/pppppppp/8/8/8/8/PPPPPPPP/NNRBBKRQ w KQkq - 0 1","nrnbbkrq/pppppppp/8/8/8/8/PPPPPPPP/NRNBBKRQ w KQkq - 0 1","nrkbbnrq/pppppppp/8/8/8/8/PPPPPPPP/NRKBBNRQ w KQkq - 0 1","nrkbbrnq/pppppppp/8/8/8/8/PPPPPPPP/NRKBBRNQ w KQkq - 0 1","rnnbbkrq/pppppppp/8/8/8/8/PPPPPPPP/RNNBBKRQ w KQkq - 0 1","rnkbbnrq/pppppppp/8/8/8/8/PPPPPPPP/RNKBBNRQ w KQkq - 0 1","rnkbbrnq/pppppppp/8/8/8/8/PPPPPPPP/RNKBBRNQ w KQkq - 0 1","rknbbnrq/pppppppp/8/8/8/8/PPPPPPPP/RKNBBNRQ w KQkq - 0 1","rknbbrnq/pppppppp/8/8/8/8/PPPPPPPP/RKNBBRNQ w KQkq - 0 1","rkrbbnnq/pppppppp/8/8/8/8/PPPPPPPP/RKRBBNNQ w KQkq - 0 1","qnnrbbkr/pppppppp/8/8/8/8/PPPPPPPP/QNNRBBKR w KQkq - 0 1","qnrnbbkr/pppppppp/8/8/8/8/PPPPPPPP/QNRNBBKR w KQkq - 0 1","qnrkbbnr/pppppppp/8/8/8/8/PPPPPPPP/QNRKBBNR w KQkq - 0 1","qnrkbbrn/pppppppp/8/8/8/8/PPPPPPPP/QNRKBBRN w KQkq - 0 1","qrnnbbkr/pppppppp/8/8/8/8/PPPPPPPP/QRNNBBKR w KQkq - 0 1","qrnkbbnr/pppppppp/8/8/8/8/PPPPPPPP/QRNKBBNR w KQkq - 0 1","qrnkbbrn/pppppppp/8/8/8/8/PPPPPPPP/QRNKBBRN w KQkq - 0 1","qrknbbnr/pppppppp/8/8/8/8/PPPPPPPP/QRKNBBNR w KQkq - 0 1","qrknbbrn/pppppppp/8/8/8/8/PPPPPPPP/QRKNBBRN w KQkq - 0 1","qrkrbbnn/pppppppp/8/8/8/8/PPPPPPPP/QRKRBBNN w KQkq - 0 1","nqnrbbkr/pppppppp/8/8/8/8/PPPPPPPP/NQNRBBKR w KQkq - 0 1","nqrnbbkr/pppppppp/8/8/8/8/PPPPPPPP/NQRNBBKR w KQkq - 0 1","nqrkbbnr/pppppppp/8/8/8/8/PPPPPPPP/NQRKBBNR w KQkq - 0 1","nqrkbbrn/pppppppp/8/8/8/8/PPPPPPPP/NQRKBBRN w KQkq - 0 1","rqnnbbkr/pppppppp/8/8/8/8/PPPPPPPP/RQNNBBKR w KQkq - 0 1","rqnkbbnr/pppppppp/8/8/8/8/PPPPPPPP/RQNKBBNR w KQkq - 0 1","rqnkbbrn/pppppppp/8/8/8/8/PPPPPPPP/RQNKBBRN w KQkq - 0 1","rqknbbnr/pppppppp/8/8/8/8/PPPPPPPP/RQKNBBNR w KQkq - 0 1","rqknbbrn/pppppppp/8/8/8/8/PPPPPPPP/RQKNBBRN w KQkq - 0 1","rqkrbbnn/pppppppp/8/8/8/8/PPPPPPPP/RQKRBBNN w KQkq - 0 1","nnqrbbkr/pppppppp/8/8/8/8/PPPPPPPP/NNQRBBKR w KQkq - 0 1","nrqnbbkr/pppppppp/8/8/8/8/PPPPPPPP/NRQNBBKR w KQkq - 0 1","nrqkbbnr/pppppppp/8/8/8/8/PPPPPPPP/NRQKBBNR w KQkq - 0 1","nrqkbbrn/pppppppp/8/8/8/8/PPPPPPPP/NRQKBBRN w KQkq - 0 1","rnqnbbkr/pppppppp/8/8/8/8/PPPPPPPP/RNQNBBKR w KQkq - 0 1","rnqkbbnr/pppppppp/8/8/8/8/PPPPPPPP/RNQKBBNR w KQkq - 0 1","rnqkbbrn/pppppppp/8/8/8/8/PPPPPPPP/RNQKBBRN w KQkq - 0 1","rkqnbbnr/pppppppp/8/8/8/8/PPPPPPPP/RKQNBBNR w KQkq - 0 1","rkqnbbrn/pppppppp/8/8/8/8/PPPPPPPP/RKQNBBRN w KQkq - 0 1","rkqrbbnn/pppppppp/8/8/8/8/PPPPPPPP/RKQRBBNN w KQkq - 0 1","nnrqbbkr/pppppppp/8/8/8/8/PPPPPPPP/NNRQBBKR w KQkq - 0 1","nrnqbbkr/pppppppp/8/8/8/8/PPPPPPPP/NRNQBBKR w KQkq - 0 1","nrkqbbnr/pppppppp/8/8/8/8/PPPPPPPP/NRKQBBNR w KQkq - 0 1","nrkqbbrn/pppppppp/8/8/8/8/PPPPPPPP/NRKQBBRN w KQkq - 0 1","rnnqbbkr/pppppppp/8/8/8/8/PPPPPPPP/RNNQBBKR w KQkq - 0 1","rnkqbbnr/pppppppp/8/8/8/8/PPPPPPPP/RNKQBBNR w KQkq - 0 1","rnkqbbrn/pppppppp/8/8/8/8/PPPPPPPP/RNKQBBRN w KQkq - 0 1","rknqbbnr/pppppppp/8/8/8/8/PPPPPPPP/RKNQBBNR w KQkq - 0 1","rknqbbrn/pppppppp/8/8/8/8/PPPPPPPP/RKNQBBRN w KQkq - 0 1","rkrqbbnn/pppppppp/8/8/8/8/PPPPPPPP/RKRQBBNN w KQkq - 0 1","nnrkbbqr/pppppppp/8/8/8/8/PPPPPPPP/NNRKBBQR w KQkq - 0 1","nrnkbbqr/pppppppp/8/8/8/8/PPPPPPPP/NRNKBBQR w KQkq - 0 1","nrknbbqr/pppppppp/8/8/8/8/PPPPPPPP/NRKNBBQR w KQkq - 0 1","nrkrbbqn/pppppppp/8/8/8/8/PPPPPPPP/NRKRBBQN w KQkq - 0 1","rnnkbbqr/pppppppp/8/8/8/8/PPPPPPPP/RNNKBBQR w KQkq - 0 1","rnknbbqr/pppppppp/8/8/8/8/PPPPPPPP/RNKNBBQR w KQkq - 0 1","rnkrbbqn/pppppppp/8/8/8/8/PPPPPPPP/RNKRBBQN w KQkq - 0 1","rknnbbqr/pppppppp/8/8/8/8/PPPPPPPP/RKNNBBQR w KQkq - 0 1","rknrbbqn/pppppppp/8/8/8/8/PPPPPPPP/RKNRBBQN w KQkq - 0 1","rkrnbbqn/pppppppp/8/8/8/8/PPPPPPPP/RKRNBBQN w KQkq - 0 1","nnrkbbrq/pppppppp/8/8/8/8/PPPPPPPP/NNRKBBRQ w KQkq - 0 1","nrnkbbrq/pppppppp/8/8/8/8/PPPPPPPP/NRNKBBRQ w KQkq - 0 1","nrknbbrq/pppppppp/8/8/8/8/PPPPPPPP/NRKNBBRQ w KQkq - 0 1","nrkrbbnq/pppppppp/8/8/8/8/PPPPPPPP/NRKRBBNQ w KQkq - 0 1","rnnkbbrq/pppppppp/8/8/8/8/PPPPPPPP/RNNKBBRQ w KQkq - 0 1","rnknbbrq/pppppppp/8/8/8/8/PPPPPPPP/RNKNBBRQ w KQkq - 0 1","rnkrbbnq/pppppppp/8/8/8/8/PPPPPPPP/RNKRBBNQ w KQkq - 0 1","rknnbbrq/pppppppp/8/8/8/8/PPPPPPPP/RKNNBBRQ w KQkq - 0 1","rknrbbnq/pppppppp/8/8/8/8/PPPPPPPP/RKNRBBNQ w KQkq - 0 1","rkrnbbnq/pppppppp/8/8/8/8/PPPPPPPP/RKRNBBNQ w KQkq - 0 1","qnnrbkrb/pppppppp/8/8/8/8/PPPPPPPP/QNNRBKRB w KQkq - 0 1","qnrnbkrb/pppppppp/8/8/8/8/PPPPPPPP/QNRNBKRB w KQkq - 0 1","qnrkbnrb/pppppppp/8/8/8/8/PPPPPPPP/QNRKBNRB w KQkq - 0 1","qnrkbrnb/pppppppp/8/8/8/8/PPPPPPPP/QNRKBRNB w KQkq - 0 1","qrnnbkrb/pppppppp/8/8/8/8/PPPPPPPP/QRNNBKRB w KQkq - 0 1","qrnkbnrb/pppppppp/8/8/8/8/PPPPPPPP/QRNKBNRB w KQkq - 0 1","qrnkbrnb/pppppppp/8/8/8/8/PPPPPPPP/QRNKBRNB w KQkq - 0 1","qrknbnrb/pppppppp/8/8/8/8/PPPPPPPP/QRKNBNRB w KQkq - 0 1","qrknbrnb/pppppppp/8/8/8/8/PPPPPPPP/QRKNBRNB w KQkq - 0 1","qrkrbnnb/pppppppp/8/8/8/8/PPPPPPPP/QRKRBNNB w KQkq - 0 1","nqnrbkrb/pppppppp/8/8/8/8/PPPPPPPP/NQNRBKRB w KQkq - 0 1","nqrnbkrb/pppppppp/8/8/8/8/PPPPPPPP/NQRNBKRB w KQkq - 0 1","nqrkbnrb/pppppppp/8/8/8/8/PPPPPPPP/NQRKBNRB w KQkq - 0 1","nqrkbrnb/pppppppp/8/8/8/8/PPPPPPPP/NQRKBRNB w KQkq - 0 1","rqnnbkrb/pppppppp/8/8/8/8/PPPPPPPP/RQNNBKRB w KQkq - 0 1","rqnkbnrb/pppppppp/8/8/8/8/PPPPPPPP/RQNKBNRB w KQkq - 0 1","rqnkbrnb/pppppppp/8/8/8/8/PPPPPPPP/RQNKBRNB w KQkq - 0 1","rqknbnrb/pppppppp/8/8/8/8/PPPPPPPP/RQKNBNRB w KQkq - 0 1","rqknbrnb/pppppppp/8/8/8/8/PPPPPPPP/RQKNBRNB w KQkq - 0 1","rqkrbnnb/pppppppp/8/8/8/8/PPPPPPPP/RQKRBNNB w KQkq - 0 1","nnqrbkrb/pppppppp/8/8/8/8/PPPPPPPP/NNQRBKRB w KQkq - 0 1","nrqnbkrb/pppppppp/8/8/8/8/PPPPPPPP/NRQNBKRB w KQkq - 0 1","nrqkbnrb/pppppppp/8/8/8/8/PPPPPPPP/NRQKBNRB w KQkq - 0 1","nrqkbrnb/pppppppp/8/8/8/8/PPPPPPPP/NRQKBRNB w KQkq - 0 1","rnqnbkrb/pppppppp/8/8/8/8/PPPPPPPP/RNQNBKRB w KQkq - 0 1","rnqkbnrb/pppppppp/8/8/8/8/PPPPPPPP/RNQKBNRB w KQkq - 0 1","rnqkbrnb/pppppppp/8/8/8/8/PPPPPPPP/RNQKBRNB w KQkq - 0 1","rkqnbnrb/pppppppp/8/8/8/8/PPPPPPPP/RKQNBNRB w KQkq - 0 1","rkqnbrnb/pppppppp/8/8/8/8/PPPPPPPP/RKQNBRNB w KQkq - 0 1","rkqrbnnb/pppppppp/8/8/8/8/PPPPPPPP/RKQRBNNB w KQkq - 0 1","nnrqbkrb/pppppppp/8/8/8/8/PPPPPPPP/NNRQBKRB w KQkq - 0 1","nrnqbkrb/pppppppp/8/8/8/8/PPPPPPPP/NRNQBKRB w KQkq - 0 1","nrkqbnrb/pppppppp/8/8/8/8/PPPPPPPP/NRKQBNRB w KQkq - 0 1","nrkqbrnb/pppppppp/8/8/8/8/PPPPPPPP/NRKQBRNB w KQkq - 0 1","rnnqbkrb/pppppppp/8/8/8/8/PPPPPPPP/RNNQBKRB w KQkq - 0 1","rnkqbnrb/pppppppp/8/8/8/8/PPPPPPPP/RNKQBNRB w KQkq - 0 1","rnkqbrnb/pppppppp/8/8/8/8/PPPPPPPP/RNKQBRNB w KQkq - 0 1","rknqbnrb/pppppppp/8/8/8/8/PPPPPPPP/RKNQBNRB w KQkq - 0 1","rknqbrnb/pppppppp/8/8/8/8/PPPPPPPP/RKNQBRNB w KQkq - 0 1","rkrqbnnb/pppppppp/8/8/8/8/PPPPPPPP/RKRQBNNB w KQkq - 0 1","nnrkbqrb/pppppppp/8/8/8/8/PPPPPPPP/NNRKBQRB w KQkq - 0 1","nrnkbqrb/pppppppp/8/8/8/8/PPPPPPPP/NRNKBQRB w KQkq - 0 1","nrknbqrb/pppppppp/8/8/8/8/PPPPPPPP/NRKNBQRB w KQkq - 0 1","nrkrbqnb/pppppppp/8/8/8/8/PPPPPPPP/NRKRBQNB w KQkq - 0 1","rnnkbqrb/pppppppp/8/8/8/8/PPPPPPPP/RNNKBQRB w KQkq - 0 1","rnknbqrb/pppppppp/8/8/8/8/PPPPPPPP/RNKNBQRB w KQkq - 0 1","rnkrbqnb/pppppppp/8/8/8/8/PPPPPPPP/RNKRBQNB w KQkq - 0 1","rknnbqrb/pppppppp/8/8/8/8/PPPPPPPP/RKNNBQRB w KQkq - 0 1","rknrbqnb/pppppppp/8/8/8/8/PPPPPPPP/RKNRBQNB w KQkq - 0 1","rkrnbqnb/pppppppp/8/8/8/8/PPPPPPPP/RKRNBQNB w KQkq - 0 1","nnrkbrqb/pppppppp/8/8/8/8/PPPPPPPP/NNRKBRQB w KQkq - 0 1","nrnkbrqb/pppppppp/8/8/8/8/PPPPPPPP/NRNKBRQB w KQkq - 0 1","nrknbrqb/pppppppp/8/8/8/8/PPPPPPPP/NRKNBRQB w KQkq - 0 1","nrkrbnqb/pppppppp/8/8/8/8/PPPPPPPP/NRKRBNQB w KQkq - 0 1","rnnkbrqb/pppppppp/8/8/8/8/PPPPPPPP/RNNKBRQB w KQkq - 0 1","rnknbrqb/pppppppp/8/8/8/8/PPPPPPPP/RNKNBRQB w KQkq - 0 1","rnkrbnqb/pppppppp/8/8/8/8/PPPPPPPP/RNKRBNQB w KQkq - 0 1","rknnbrqb/pppppppp/8/8/8/8/PPPPPPPP/RKNNBRQB w KQkq - 0 1","rknrbnqb/pppppppp/8/8/8/8/PPPPPPPP/RKNRBNQB w KQkq - 0 1","rkrnbnqb/pppppppp/8/8/8/8/PPPPPPPP/RKRNBNQB w KQkq - 0 1","qbnnrkbr/pppppppp/8/8/8/8/PPPPPPPP/QBNNRKBR w KQkq - 0 1","qbnrnkbr/pppppppp/8/8/8/8/PPPPPPPP/QBNRNKBR w KQkq - 0 1","qbnrknbr/pppppppp/8/8/8/8/PPPPPPPP/QBNRKNBR w KQkq - 0 1","qbnrkrbn/pppppppp/8/8/8/8/PPPPPPPP/QBNRKRBN w KQkq - 0 1","qbrnnkbr/pppppppp/8/8/8/8/PPPPPPPP/QBRNNKBR w KQkq - 0 1","qbrnknbr/pppppppp/8/8/8/8/PPPPPPPP/QBRNKNBR w KQkq - 0 1","qbrnkrbn/pppppppp/8/8/8/8/PPPPPPPP/QBRNKRBN w KQkq - 0 1","qbrknnbr/pppppppp/8/8/8/8/PPPPPPPP/QBRKNNBR w KQkq - 0 1","qbrknrbn/pppppppp/8/8/8/8/PPPPPPPP/QBRKNRBN w KQkq - 0 1","qbrkrnbn/pppppppp/8/8/8/8/PPPPPPPP/QBRKRNBN w KQkq - 0 1","nbqnrkbr/pppppppp/8/8/8/8/PPPPPPPP/NBQNRKBR w KQkq - 0 1","nbqrnkbr/pppppppp/8/8/8/8/PPPPPPPP/NBQRNKBR w KQkq - 0 1","nbqrknbr/pppppppp/8/8/8/8/PPPPPPPP/NBQRKNBR w KQkq - 0 1","nbqrkrbn/pppppppp/8/8/8/8/PPPPPPPP/NBQRKRBN w KQkq - 0 1","rbqnnkbr/pppppppp/8/8/8/8/PPPPPPPP/RBQNNKBR w KQkq - 0 1","rbqnknbr/pppppppp/8/8/8/8/PPPPPPPP/RBQNKNBR w KQkq - 0 1","rbqnkrbn/pppppppp/8/8/8/8/PPPPPPPP/RBQNKRBN w KQkq - 0 1","rbqknnbr/pppppppp/8/8/8/8/PPPPPPPP/RBQKNNBR w KQkq - 0 1","rbqknrbn/pppppppp/8/8/8/8/PPPPPPPP/RBQKNRBN w KQkq - 0 1","rbqkrnbn/pppppppp/8/8/8/8/PPPPPPPP/RBQKRNBN w KQkq - 0 1","nbnqrkbr/pppppppp/8/8/8/8/PPPPPPPP/NBNQRKBR w KQkq - 0 1","nbrqnkbr/pppppppp/8/8/8/8/PPPPPPPP/NBRQNKBR w KQkq - 0 1","nbrqknbr/pppppppp/8/8/8/8/PPPPPPPP/NBRQKNBR w KQkq - 0 1","nbrqkrbn/pppppppp/8/8/8/8/PPPPPPPP/NBRQKRBN w KQkq - 0 1","rbnqnkbr/pppppppp/8/8/8/8/PPPPPPPP/RBNQNKBR w KQkq - 0 1","rbnqknbr/pppppppp/8/8/8/8/PPPPPPPP/RBNQKNBR w KQkq - 0 1","rbnqkrbn/pppppppp/8/8/8/8/PPPPPPPP/RBNQKRBN w KQkq - 0 1","rbkqnnbr/pppppppp/8/8/8/8/PPPPPPPP/RBKQNNBR w KQkq - 0 1","rbkqnrbn/pppppppp/8/8/8/8/PPPPPPPP/RBKQNRBN w KQkq - 0 1","rbkqrnbn/pppppppp/8/8/8/8/PPPPPPPP/RBKQRNBN w KQkq - 0 1","nbnrqkbr/pppppppp/8/8/8/8/PPPPPPPP/NBNRQKBR w KQkq - 0 1","nbrnqkbr/pppppppp/8/8/8/8/PPPPPPPP/NBRNQKBR w KQkq - 0 1","nbrkqnbr/pppppppp/8/8/8/8/PPPPPPPP/NBRKQNBR w KQkq - 0 1","nbrkqrbn/pppppppp/8/8/8/8/PPPPPPPP/NBRKQRBN w KQkq - 0 1","rbnnqkbr/pppppppp/8/8/8/8/PPPPPPPP/RBNNQKBR w KQkq - 0 1","rbnkqnbr/pppppppp/8/8/8/8/PPPPPPPP/RBNKQNBR w KQkq - 0 1","rbnkqrbn/pppppppp/8/8/8/8/PPPPPPPP/RBNKQRBN w KQkq - 0 1","rbknqnbr/pppppppp/8/8/8/8/PPPPPPPP/RBKNQNBR w KQkq - 0 1","rbknqrbn/pppppppp/8/8/8/8/PPPPPPPP/RBKNQRBN w KQkq - 0 1","rbkrqnbn/pppppppp/8/8/8/8/PPPPPPPP/RBKRQNBN w KQkq - 0 1","nbnrkqbr/pppppppp/8/8/8/8/PPPPPPPP/NBNRKQBR w KQkq - 0 1","nbrnkqbr/pppppppp/8/8/8/8/PPPPPPPP/NBRNKQBR w KQkq - 0 1","nbrknqbr/pppppppp/8/8/8/8/PPPPPPPP/NBRKNQBR w KQkq - 0 1","nbrkrqbn/pppppppp/8/8/8/8/PPPPPPPP/NBRKRQBN w KQkq - 0 1","rbnnkqbr/pppppppp/8/8/8/8/PPPPPPPP/RBNNKQBR w KQkq - 0 1","rbnknqbr/pppppppp/8/8/8/8/PPPPPPPP/RBNKNQBR w KQkq - 0 1","rbnkrqbn/pppppppp/8/8/8/8/PPPPPPPP/RBNKRQBN w KQkq - 0 1","rbknnqbr/pppppppp/8/8/8/8/PPPPPPPP/RBKNNQBR w KQkq - 0 1","rbknrqbn/pppppppp/8/8/8/8/PPPPPPPP/RBKNRQBN w KQkq - 0 1","rbkrnqbn/pppppppp/8/8/8/8/PPPPPPPP/RBKRNQBN w KQkq - 0 1","nbnrkrbq/pppppppp/8/8/8/8/PPPPPPPP/NBNRKRBQ w KQkq - 0 1","nbrnkrbq/pppppppp/8/8/8/8/PPPPPPPP/NBRNKRBQ w KQkq - 0 1","nbrknrbq/pppppppp/8/8/8/8/PPPPPPPP/NBRKNRBQ w KQkq - 0 1","nbrkrnbq/pppppppp/8/8/8/8/PPPPPPPP/NBRKRNBQ w KQkq - 0 1","rbnnkrbq/pppppppp/8/8/8/8/PPPPPPPP/RBNNKRBQ w KQkq - 0 1","rbnknrbq/pppppppp/8/8/8/8/PPPPPPPP/RBNKNRBQ w KQkq - 0 1","rbnkrnbq/pppppppp/8/8/8/8/PPPPPPPP/RBNKRNBQ w KQkq - 0 1","rbknnrbq/pppppppp/8/8/8/8/PPPPPPPP/RBKNNRBQ w KQkq - 0 1","rbknrnbq/pppppppp/8/8/8/8/PPPPPPPP/RBKNRNBQ w KQkq - 0 1","rbkrnnbq/pppppppp/8/8/8/8/PPPPPPPP/RBKRNNBQ w KQkq - 0 1","qnnbrkbr/pppppppp/8/8/8/8/PPPPPPPP/QNNBRKBR w KQkq - 0 1","qnrbnkbr/pppppppp/8/8/8/8/PPPPPPPP/QNRBNKBR w KQkq - 0 1","qnrbknbr/pppppppp/8/8/8/8/PPPPPPPP/QNRBKNBR w KQkq - 0 1","qnrbkrbn/pppppppp/8/8/8/8/PPPPPPPP/QNRBKRBN w KQkq - 0 1","qrnbnkbr/pppppppp/8/8/8/8/PPPPPPPP/QRNBNKBR w KQkq - 0 1","qrnbknbr/pppppppp/8/8/8/8/PPPPPPPP/QRNBKNBR w KQkq - 0 1","qrnbkrbn/pppppppp/8/8/8/8/PPPPPPPP/QRNBKRBN w KQkq - 0 1","qrkbnnbr/pppppppp/8/8/8/8/PPPPPPPP/QRKBNNBR w KQkq - 0 1","qrkbnrbn/pppppppp/8/8/8/8/PPPPPPPP/QRKBNRBN w KQkq - 0 1","qrkbrnbn/pppppppp/8/8/8/8/PPPPPPPP/QRKBRNBN w KQkq - 0 1","nqnbrkbr/pppppppp/8/8/8/8/PPPPPPPP/NQNBRKBR w KQkq - 0 1","nqrbnkbr/pppppppp/8/8/8/8/PPPPPPPP/NQRBNKBR w KQkq - 0 1","nqrbknbr/pppppppp/8/8/8/8/PPPPPPPP/NQRBKNBR w KQkq - 0 1","nqrbkrbn/pppppppp/8/8/8/8/PPPPPPPP/NQRBKRBN w KQkq - 0 1","rqnbnkbr/pppppppp/8/8/8/8/PPPPPPPP/RQNBNKBR w KQkq - 0 1","rqnbknbr/pppppppp/8/8/8/8/PPPPPPPP/RQNBKNBR w KQkq - 0 1","rqnbkrbn/pppppppp/8/8/8/8/PPPPPPPP/RQNBKRBN w KQkq - 0 1","rqkbnnbr/pppppppp/8/8/8/8/PPPPPPPP/RQKBNNBR w KQkq - 0 1","rqkbnrbn/pppppppp/8/8/8/8/PPPPPPPP/RQKBNRBN w KQkq - 0 1","rqkbrnbn/pppppppp/8/8/8/8/PPPPPPPP/RQKBRNBN w KQkq - 0 1","nnqbrkbr/pppppppp/8/8/8/8/PPPPPPPP/NNQBRKBR w KQkq - 0 1","nrqbnkbr/pppppppp/8/8/8/8/PPPPPPPP/NRQBNKBR w KQkq - 0 1","nrqbknbr/pppppppp/8/8/8/8/PPPPPPPP/NRQBKNBR w KQkq - 0 1","nrqbkrbn/pppppppp/8/8/8/8/PPPPPPPP/NRQBKRBN w KQkq - 0 1","rnqbnkbr/pppppppp/8/8/8/8/PPPPPPPP/RNQBNKBR w KQkq - 0 1","rnqbknbr/pppppppp/8/8/8/8/PPPPPPPP/RNQBKNBR w KQkq - 0 1","rnqbkrbn/pppppppp/8/8/8/8/PPPPPPPP/RNQBKRBN w KQkq - 0 1","rkqbnnbr/pppppppp/8/8/8/8/PPPPPPPP/RKQBNNBR w KQkq - 0 1","rkqbnrbn/pppppppp/8/8/8/8/PPPPPPPP/RKQBNRBN w KQkq - 0 1","rkqbrnbn/pppppppp/8/8/8/8/PPPPPPPP/RKQBRNBN w KQkq - 0 1","nnrbqkbr/pppppppp/8/8/8/8/PPPPPPPP/NNRBQKBR w KQkq - 0 1","nrnbqkbr/pppppppp/8/8/8/8/PPPPPPPP/NRNBQKBR w KQkq - 0 1","nrkbqnbr/pppppppp/8/8/8/8/PPPPPPPP/NRKBQNBR w KQkq - 0 1","nrkbqrbn/pppppppp/8/8/8/8/PPPPPPPP/NRKBQRBN w KQkq - 0 1","rnnbqkbr/pppppppp/8/8/8/8/PPPPPPPP/RNNBQKBR w KQkq - 0 1","rnkbqnbr/pppppppp/8/8/8/8/PPPPPPPP/RNKBQNBR w KQkq - 0 1","rnkbqrbn/pppppppp/8/8/8/8/PPPPPPPP/RNKBQRBN w KQkq - 0 1","rknbqnbr/pppppppp/8/8/8/8/PPPPPPPP/RKNBQNBR w KQkq - 0 1","rknbqrbn/pppppppp/8/8/8/8/PPPPPPPP/RKNBQRBN w KQkq - 0 1","rkrbqnbn/pppppppp/8/8/8/8/PPPPPPPP/RKRBQNBN w KQkq - 0 1","nnrbkqbr/pppppppp/8/8/8/8/PPPPPPPP/NNRBKQBR w KQkq - 0 1","nrnbkqbr/pppppppp/8/8/8/8/PPPPPPPP/NRNBKQBR w KQkq - 0 1","nrkbnqbr/pppppppp/8/8/8/8/PPPPPPPP/NRKBNQBR w KQkq - 0 1","nrkbrqbn/pppppppp/8/8/8/8/PPPPPPPP/NRKBRQBN w KQkq - 0 1","rnnbkqbr/pppppppp/8/8/8/8/PPPPPPPP/RNNBKQBR w KQkq - 0 1","rnkbnqbr/pppppppp/8/8/8/8/PPPPPPPP/RNKBNQBR w KQkq - 0 1","rnkbrqbn/pppppppp/8/8/8/8/PPPPPPPP/RNKBRQBN w KQkq - 0 1","rknbnqbr/pppppppp/8/8/8/8/PPPPPPPP/RKNBNQBR w KQkq - 0 1","rknbrqbn/pppppppp/8/8/8/8/PPPPPPPP/RKNBRQBN w KQkq - 0 1","rkrbnqbn/pppppppp/8/8/8/8/PPPPPPPP/RKRBNQBN w KQkq - 0 1","nnrbkrbq/pppppppp/8/8/8/8/PPPPPPPP/NNRBKRBQ w KQkq - 0 1","nrnbkrbq/pppppppp/8/8/8/8/PPPPPPPP/NRNBKRBQ w KQkq - 0 1","nrkbnrbq/pppppppp/8/8/8/8/PPPPPPPP/NRKBNRBQ w KQkq - 0 1","nrkbrnbq/pppppppp/8/8/8/8/PPPPPPPP/NRKBRNBQ w KQkq - 0 1","rnnbkrbq/pppppppp/8/8/8/8/PPPPPPPP/RNNBKRBQ w KQkq - 0 1","rnkbnrbq/pppppppp/8/8/8/8/PPPPPPPP/RNKBNRBQ w KQkq - 0 1","rnkbrnbq/pppppppp/8/8/8/8/PPPPPPPP/RNKBRNBQ w KQkq - 0 1","rknbnrbq/pppppppp/8/8/8/8/PPPPPPPP/RKNBNRBQ w KQkq - 0 1","rknbrnbq/pppppppp/8/8/8/8/PPPPPPPP/RKNBRNBQ w KQkq - 0 1","rkrbnnbq/pppppppp/8/8/8/8/PPPPPPPP/RKRBNNBQ w KQkq - 0 1","qnnrkbbr/pppppppp/8/8/8/8/PPPPPPPP/QNNRKBBR w KQkq - 0 1","qnrnkbbr/pppppppp/8/8/8/8/PPPPPPPP/QNRNKBBR w KQkq - 0 1","qnrknbbr/pppppppp/8/8/8/8/PPPPPPPP/QNRKNBBR w KQkq - 0 1","qnrkrbbn/pppppppp/8/8/8/8/PPPPPPPP/QNRKRBBN w KQkq - 0 1","qrnnkbbr/pppppppp/8/8/8/8/PPPPPPPP/QRNNKBBR w KQkq - 0 1","qrnknbbr/pppppppp/8/8/8/8/PPPPPPPP/QRNKNBBR w KQkq - 0 1","qrnkrbbn/pppppppp/8/8/8/8/PPPPPPPP/QRNKRBBN w KQkq - 0 1","qrknnbbr/pppppppp/8/8/8/8/PPPPPPPP/QRKNNBBR w KQkq - 0 1","qrknrbbn/pppppppp/8/8/8/8/PPPPPPPP/QRKNRBBN w KQkq - 0 1","qrkrnbbn/pppppppp/8/8/8/8/PPPPPPPP/QRKRNBBN w KQkq - 0 1","nqnrkbbr/pppppppp/8/8/8/8/PPPPPPPP/NQNRKBBR w KQkq - 0 1","nqrnkbbr/pppppppp/8/8/8/8/PPPPPPPP/NQRNKBBR w KQkq - 0 1","nqrknbbr/pppppppp/8/8/8/8/PPPPPPPP/NQRKNBBR w KQkq - 0 1","nqrkrbbn/pppppppp/8/8/8/8/PPPPPPPP/NQRKRBBN w KQkq - 0 1","rqnnkbbr/pppppppp/8/8/8/8/PPPPPPPP/RQNNKBBR w KQkq - 0 1","rqnknbbr/pppppppp/8/8/8/8/PPPPPPPP/RQNKNBBR w KQkq - 0 1","rqnkrbbn/pppppppp/8/8/8/8/PPPPPPPP/RQNKRBBN w KQkq - 0 1","rqknnbbr/pppppppp/8/8/8/8/PPPPPPPP/RQKNNBBR w KQkq - 0 1","rqknrbbn/pppppppp/8/8/8/8/PPPPPPPP/RQKNRBBN w KQkq - 0 1","rqkrnbbn/pppppppp/8/8/8/8/PPPPPPPP/RQKRNBBN w KQkq - 0 1","nnqrkbbr/pppppppp/8/8/8/8/PPPPPPPP/NNQRKBBR w KQkq - 0 1","nrqnkbbr/pppppppp/8/8/8/8/PPPPPPPP/NRQNKBBR w KQkq - 0 1","nrqknbbr/pppppppp/8/8/8/8/PPPPPPPP/NRQKNBBR w KQkq - 0 1","nrqkrbbn/pppppppp/8/8/8/8/PPPPPPPP/NRQKRBBN w KQkq - 0 1","rnqnkbbr/pppppppp/8/8/8/8/PPPPPPPP/RNQNKBBR w KQkq - 0 1","rnqknbbr/pppppppp/8/8/8/8/PPPPPPPP/RNQKNBBR w KQkq - 0 1","rnqkrbbn/pppppppp/8/8/8/8/PPPPPPPP/RNQKRBBN w KQkq - 0 1","rkqnnbbr/pppppppp/8/8/8/8/PPPPPPPP/RKQNNBBR w KQkq - 0 1","rkqnrbbn/pppppppp/8/8/8/8/PPPPPPPP/RKQNRBBN w KQkq - 0 1","rkqrnbbn/pppppppp/8/8/8/8/PPPPPPPP/RKQRNBBN w KQkq - 0 1","nnrqkbbr/pppppppp/8/8/8/8/PPPPPPPP/NNRQKBBR w KQkq - 0 1","nrnqkbbr/pppppppp/8/8/8/8/PPPPPPPP/NRNQKBBR w KQkq - 0 1","nrkqnbbr/pppppppp/8/8/8/8/PPPPPPPP/NRKQNBBR w KQkq - 0 1","nrkqrbbn/pppppppp/8/8/8/8/PPPPPPPP/NRKQRBBN w KQkq - 0 1","rnnqkbbr/pppppppp/8/8/8/8/PPPPPPPP/RNNQKBBR w KQkq - 0 1","rnkqnbbr/pppppppp/8/8/8/8/PPPPPPPP/RNKQNBBR w KQkq - 0 1","rnkqrbbn/pppppppp/8/8/8/8/PPPPPPPP/RNKQRBBN w KQkq - 0 1","rknqnbbr/pppppppp/8/8/8/8/PPPPPPPP/RKNQNBBR w KQkq - 0 1","rknqrbbn/pppppppp/8/8/8/8/PPPPPPPP/RKNQRBBN w KQkq - 0 1","rkrqnbbn/pppppppp/8/8/8/8/PPPPPPPP/RKRQNBBN w KQkq - 0 1","nnrkqbbr/pppppppp/8/8/8/8/PPPPPPPP/NNRKQBBR w KQkq - 0 1","nrnkqbbr/pppppppp/8/8/8/8/PPPPPPPP/NRNKQBBR w KQkq - 0 1","nrknqbbr/pppppppp/8/8/8/8/PPPPPPPP/NRKNQBBR w KQkq - 0 1","nrkrqbbn/pppppppp/8/8/8/8/PPPPPPPP/NRKRQBBN w KQkq - 0 1","rnnkqbbr/pppppppp/8/8/8/8/PPPPPPPP/RNNKQBBR w KQkq - 0 1","rnknqbbr/pppppppp/8/8/8/8/PPPPPPPP/RNKNQBBR w KQkq - 0 1","rnkrqbbn/pppppppp/8/8/8/8/PPPPPPPP/RNKRQBBN w KQkq - 0 1","rknnqbbr/pppppppp/8/8/8/8/PPPPPPPP/RKNNQBBR w KQkq - 0 1","rknrqbbn/pppppppp/8/8/8/8/PPPPPPPP/RKNRQBBN w KQkq - 0 1","rkrnqbbn/pppppppp/8/8/8/8/PPPPPPPP/RKRNQBBN w KQkq - 0 1","nnrkrbbq/pppppppp/8/8/8/8/PPPPPPPP/NNRKRBBQ w KQkq - 0 1","nrnkrbbq/pppppppp/8/8/8/8/PPPPPPPP/NRNKRBBQ w KQkq - 0 1","nrknrbbq/pppppppp/8/8/8/8/PPPPPPPP/NRKNRBBQ w KQkq - 0 1","nrkrnbbq/pppppppp/8/8/8/8/PPPPPPPP/NRKRNBBQ w KQkq - 0 1","rnnkrbbq/pppppppp/8/8/8/8/PPPPPPPP/RNNKRBBQ w KQkq - 0 1","rnknrbbq/pppppppp/8/8/8/8/PPPPPPPP/RNKNRBBQ w KQkq - 0 1","rnkrnbbq/pppppppp/8/8/8/8/PPPPPPPP/RNKRNBBQ w KQkq - 0 1","rknnrbbq/pppppppp/8/8/8/8/PPPPPPPP/RKNNRBBQ w KQkq - 0 1","rknrnbbq/pppppppp/8/8/8/8/PPPPPPPP/RKNRNBBQ w KQkq - 0 1","rkrnnbbq/pppppppp/8/8/8/8/PPPPPPPP/RKRNNBBQ w KQkq - 0 1","qnnrkrbb/pppppppp/8/8/8/8/PPPPPPPP/QNNRKRBB w KQkq - 0 1","qnrnkrbb/pppppppp/8/8/8/8/PPPPPPPP/QNRNKRBB w KQkq - 0 1","qnrknrbb/pppppppp/8/8/8/8/PPPPPPPP/QNRKNRBB w KQkq - 0 1","qnrkrnbb/pppppppp/8/8/8/8/PPPPPPPP/QNRKRNBB w KQkq - 0 1","qrnnkrbb/pppppppp/8/8/8/8/PPPPPPPP/QRNNKRBB w KQkq - 0 1","qrnknrbb/pppppppp/8/8/8/8/PPPPPPPP/QRNKNRBB w KQkq - 0 1","qrnkrnbb/pppppppp/8/8/8/8/PPPPPPPP/QRNKRNBB w KQkq - 0 1","qrknnrbb/pppppppp/8/8/8/8/PPPPPPPP/QRKNNRBB w KQkq - 0 1","qrknrnbb/pppppppp/8/8/8/8/PPPPPPPP/QRKNRNBB w KQkq - 0 1","qrkrnnbb/pppppppp/8/8/8/8/PPPPPPPP/QRKRNNBB w KQkq - 0 1","nqnrkrbb/pppppppp/8/8/8/8/PPPPPPPP/NQNRKRBB w KQkq - 0 1","nqrnkrbb/pppppppp/8/8/8/8/PPPPPPPP/NQRNKRBB w KQkq - 0 1","nqrknrbb/pppppppp/8/8/8/8/PPPPPPPP/NQRKNRBB w KQkq - 0 1","nqrkrnbb/pppppppp/8/8/8/8/PPPPPPPP/NQRKRNBB w KQkq - 0 1","rqnnkrbb/pppppppp/8/8/8/8/PPPPPPPP/RQNNKRBB w KQkq - 0 1","rqnknrbb/pppppppp/8/8/8/8/PPPPPPPP/RQNKNRBB w KQkq - 0 1","rqnkrnbb/pppppppp/8/8/8/8/PPPPPPPP/RQNKRNBB w KQkq - 0 1","rqknnrbb/pppppppp/8/8/8/8/PPPPPPPP/RQKNNRBB w KQkq - 0 1","rqknrnbb/pppppppp/8/8/8/8/PPPPPPPP/RQKNRNBB w KQkq - 0 1","rqkrnnbb/pppppppp/8/8/8/8/PPPPPPPP/RQKRNNBB w KQkq - 0 1","nnqrkrbb/pppppppp/8/8/8/8/PPPPPPPP/NNQRKRBB w KQkq - 0 1","nrqnkrbb/pppppppp/8/8/8/8/PPPPPPPP/NRQNKRBB w KQkq - 0 1","nrqknrbb/pppppppp/8/8/8/8/PPPPPPPP/NRQKNRBB w KQkq - 0 1","nrqkrnbb/pppppppp/8/8/8/8/PPPPPPPP/NRQKRNBB w KQkq - 0 1","rnqnkrbb/pppppppp/8/8/8/8/PPPPPPPP/RNQNKRBB w KQkq - 0 1","rnqknrbb/pppppppp/8/8/8/8/PPPPPPPP/RNQKNRBB w KQkq - 0 1","rnqkrnbb/pppppppp/8/8/8/8/PPPPPPPP/RNQKRNBB w KQkq - 0 1","rkqnnrbb/pppppppp/8/8/8/8/PPPPPPPP/RKQNNRBB w KQkq - 0 1","rkqnrnbb/pppppppp/8/8/8/8/PPPPPPPP/RKQNRNBB w KQkq - 0 1","rkqrnnbb/pppppppp/8/8/8/8/PPPPPPPP/RKQRNNBB w KQkq - 0 1","nnrqkrbb/pppppppp/8/8/8/8/PPPPPPPP/NNRQKRBB w KQkq - 0 1","nrnqkrbb/pppppppp/8/8/8/8/PPPPPPPP/NRNQKRBB w KQkq - 0 1","nrkqnrbb/pppppppp/8/8/8/8/PPPPPPPP/NRKQNRBB w KQkq - 0 1","nrkqrnbb/pppppppp/8/8/8/8/PPPPPPPP/NRKQRNBB w KQkq - 0 1","rnnqkrbb/pppppppp/8/8/8/8/PPPPPPPP/RNNQKRBB w KQkq - 0 1","rnkqnrbb/pppppppp/8/8/8/8/PPPPPPPP/RNKQNRBB w KQkq - 0 1","rnkqrnbb/pppppppp/8/8/8/8/PPPPPPPP/RNKQRNBB w KQkq - 0 1","rknqnrbb/pppppppp/8/8/8/8/PPPPPPPP/RKNQNRBB w KQkq - 0 1","rknqrnbb/pppppppp/8/8/8/8/PPPPPPPP/RKNQRNBB w KQkq - 0 1","rkrqnnbb/pppppppp/8/8/8/8/PPPPPPPP/RKRQNNBB w KQkq - 0 1","nnrkqrbb/pppppppp/8/8/8/8/PPPPPPPP/NNRKQRBB w KQkq - 0 1","nrnkqrbb/pppppppp/8/8/8/8/PPPPPPPP/NRNKQRBB w KQkq - 0 1","nrknqrbb/pppppppp/8/8/8/8/PPPPPPPP/NRKNQRBB w KQkq - 0 1","nrkrqnbb/pppppppp/8/8/8/8/PPPPPPPP/NRKRQNBB w KQkq - 0 1","rnnkqrbb/pppppppp/8/8/8/8/PPPPPPPP/RNNKQRBB w KQkq - 0 1","rnknqrbb/pppppppp/8/8/8/8/PPPPPPPP/RNKNQRBB w KQkq - 0 1","rnkrqnbb/pppppppp/8/8/8/8/PPPPPPPP/RNKRQNBB w KQkq - 0 1","rknnqrbb/pppppppp/8/8/8/8/PPPPPPPP/RKNNQRBB w KQkq - 0 1","rknrqnbb/pppppppp/8/8/8/8/PPPPPPPP/RKNRQNBB w KQkq - 0 1","rkrnqnbb/pppppppp/8/8/8/8/PPPPPPPP/RKRNQNBB w KQkq - 0 1","nnrkrqbb/pppppppp/8/8/8/8/PPPPPPPP/NNRKRQBB w KQkq - 0 1","nrnkrqbb/pppppppp/8/8/8/8/PPPPPPPP/NRNKRQBB w KQkq - 0 1","nrknrqbb/pppppppp/8/8/8/8/PPPPPPPP/NRKNRQBB w KQkq - 0 1","nrkrnqbb/pppppppp/8/8/8/8/PPPPPPPP/NRKRNQBB w KQkq - 0 1","rnnkrqbb/pppppppp/8/8/8/8/PPPPPPPP/RNNKRQBB w KQkq - 0 1","rnknrqbb/pppppppp/8/8/8/8/PPPPPPPP/RNKNRQBB w KQkq - 0 1","rnkrnqbb/pppppppp/8/8/8/8/PPPPPPPP/RNKRNQBB w KQkq - 0 1","rknnrqbb/pppppppp/8/8/8/8/PPPPPPPP/RKNNRQBB w KQkq - 0 1","rknrnqbb/pppppppp/8/8/8/8/PPPPPPPP/RKNRNQBB w KQkq - 0 1","rkrnnqbb/pppppppp/8/8/8/8/PPPPPPPP/RKRNNQBB w KQkq - 0 1"]

      //console.log(fs_legal_fen.length)
      const random = Math.floor(Math.random() * fs_legal_fen.length);
      console.log(random, fs_legal_fen[random]);

      this.game.load(fs_legal_fen[random])
      this.board.set({
        fen: this.game.fen(),
        turnColor: this.toColor(),
        showThreats: true,
        movable: {
          color: this.toColor(),
          dests: this.possibleMoves(),
          events: { after: this.userPlay()},
    }})

      // this.game.move({from: orig, to: dest, promotion: this.promoteTo}) // promote to queen for simplicity
      //   this.board.set({
      //     fen: this.game.fen()
      //   })

      // console.log(fs_legal_fen.sample())

    },

    async test_preformance(){
      //upgrade node to 19 to add pref-hooks but use before
      // const observer = new PerformanceObserver(list => list.getEntries().forEach(entry => console.info(entry)));
      //   observer.observe({buffered: true, entryTypes: ['function']});

      //   const wrapped = performance.timerify(this.turn_on_magnet);
      //   await wrapped();
      const start = performance.now();
      await this.turn_on_magnet();
      const stop = performance.now();
      const inSeconds = (stop - start) / 1000;
      const rounded = Number(inSeconds).toFixed(3);
      console.log(`magnet_toggle_timer: ${rounded}s`);
    },

    try_stockfish(){
      console.log("tried Stockfish");
    },

    /**
     * @description: This function turns on the magnet head heater to 100 degrees
     * @param {type} 
     * @returns: 
     */
    turn_on_magnet() {
      axios({
        method: "post",
        url: "http://192.168.1.5/printer/gcode/script?script=" + `
        SET_HEATER_TEMPERATURE HEATER=mag_head TARGET=100;
        `,
        //data: bodyFormData,
        //headers: { "Content-Type": "multipart/form-data" },
      })
      // eslint-disable-next-line
        .then(function (response) {
          //handle success
          //console.log(response);
        })
        // eslint-disable-next-line
        .catch(function (response) {
          //handle error
          //console.log(response);
        });
    },

    /**
     * @description: This function turns off the magnet head heater.
     * @param {type} 
     * @returns: 
     */
    turn_off_magnet() {
      axios({
        method: "post",
        url: "http://192.168.1.5/printer/gcode/script?script=" + `
        SET_HEATER_TEMPERATURE HEATER=mag_head TARGET=0;
        `,
        //data: bodyFormData,
        //headers: { "Content-Type": "multipart/form-data" },
      })
      // eslint-disable-next-line
        .then(function (response) {
          //handle success
          //console.log(response);
        })
        // eslint-disable-next-line
        .catch(function (response) {
          //handle error
          //console.log(response);
        });
    },

    /**
     * @description: This function is used to toggle the polarity of the magnet.
     * @param {type} 
     * @returns: 
     */
    toggle_magnet_polarity(){
      var that = this;
      axios({
        method: "get",
        url: "http://192.168.1.4/toggle",
        //data: bodyFormData,
        //headers: { "Content-Type": "multipart/form-data" },
      })
      // eslint-disable-next-line
        .then(function (response) {
          console.log("current mag state")
          console.log(that.magnet_state);
          that.magnet_state = !that.magnet_state;
          //handle success
          //console.log(response);
        })
        // eslint-disable-next-line
        .catch(function (response) {
          //handle error
          //console.log(response);
        });
    },

    /**
     * @description: This function sends a single gcode command to the printer.
     * @param {string} send_code - The gcode command to be sent to the printer.
     */
    send_single_gcode(send_code) {
      axios({
        method: "post",
        url: "http://192.168.1.5/printer/gcode/script?script=" + send_code,
        //data: bodyFormData,
        //headers: { "Content-Type": "multipart/form-data" },
      })
        .then(function () {
          //handle success
          //console.log(response);
        })
        .catch(function (response) {
          //handle error
          console.log(response);
        });
    },

    /**
     * @description: This function preforms a series of movements that simulate the movement of a pawn in chess.
     * @param {number} loop_iterations - The number of times the function will run.
     * @param {number} mag_toggle_time - The time in milliseconds that the magnet will be on or off.
     * @param {number} short_move_time - The time in milliseconds that the robot will move a short distance.
     * @param {number} slide_mode_time - The time in milliseconds that the robot will move a long distance.
     */
    async dancing_pawns(loop_iterations , mag_toggle_time , short_move_time , slide_mode_time) { //, mag_toggle_time , short_move_time , slide_mode_time
      // var mag_toggle_time = 2800;
      // var short_move_time = 500;
      // var slide_mode_time = 2300;
      var move_speed = "F5000";
      var short_move_speed = "F10000";
      var slide_move_speed = "F9000";
      for (let index = 0; index < loop_iterations; index++) {
        console.log("running " + index)
        //const element = array[index];
        this.send_single_gcode("G1 X75 Y150" + move_speed);
        await new Promise(resolve => setTimeout(resolve, 5000));
        this.turn_on_magnet();
        await new Promise(resolve => setTimeout(resolve, short_move_time));
        this.send_single_gcode("G1 X75 Y150" + short_move_speed); //PAwn Hold 1 middle good
        await new Promise(resolve => setTimeout(resolve, short_move_time));
        this.send_single_gcode("G1 X75 Y110" + short_move_speed); //Pawn 1 slot good
        await new Promise(resolve => setTimeout(resolve, short_move_time));
        this.send_single_gcode("G1 X275 Y110" + slide_move_speed); //PAwn slide 1 good
        await new Promise(resolve => setTimeout(resolve, slide_mode_time));
        this.turn_off_magnet();
        await new Promise(resolve => setTimeout(resolve, mag_toggle_time));
        this.send_single_gcode("G1 X275 Y150" + short_move_speed); //PAwn Hold 2 middle good
        await new Promise(resolve => setTimeout(resolve, short_move_time));
        this.turn_on_magnet();
        await new Promise(resolve => setTimeout(resolve, mag_toggle_time));
        this.send_single_gcode("G1 X275 Y190" + short_move_speed); //Pawn 2 Slot good
        await new Promise(resolve => setTimeout(resolve, short_move_time));
        this.turn_off_magnet();
        await new Promise(resolve => setTimeout(resolve, mag_toggle_time));
        this.send_single_gcode("G1 X275 Y110" + short_move_speed); //good
        await new Promise(resolve => setTimeout(resolve, short_move_time));
        this.turn_on_magnet();
        await new Promise(resolve => setTimeout(resolve, mag_toggle_time));
        this.send_single_gcode("G1 X275 Y150" + short_move_speed); //PAwn Hold 2 middle
        await new Promise(resolve => setTimeout(resolve, short_move_time));
        this.turn_off_magnet();
        await new Promise(resolve => setTimeout(resolve, mag_toggle_time));
        this.send_single_gcode("G1 X275 Y190" + short_move_speed); //Pawn 2 Slot
        await new Promise(resolve => setTimeout(resolve, short_move_time));
        this.turn_on_magnet();
        await new Promise(resolve => setTimeout(resolve, mag_toggle_time));
        this.send_single_gcode("G1 X75 Y190" + slide_move_speed); //PAwn slide 2
        await new Promise(resolve => setTimeout(resolve, slide_mode_time));
        this.send_single_gcode("G1 X75 Y150" + short_move_speed); //PAwn Hold 1 middle
        await new Promise(resolve => setTimeout(resolve, short_move_time));
        this.turn_off_magnet();
      }
    },

    async draw_vector(){
      var multi_gcode_obj = 
      [
        ["G1","F8000",""  ],
  ["G1","X280.195","Y59.536"  ],
  ["G1","X258.368","Y80.423"  ],
  ["G1","X254.286","Y84.428"  ],
  ["G1","X246.225","Y92.514"  ],
  ["G1","X242.143","Y96.506"  ],
  ["G1","X235.653","Y102.662"  ],
  ["G1","X225.866","Y111.830"  ],
  ["G1","X219.389","Y117.985"  ],
  ["G1","X216.182","Y121.102"  ],
  ["G1","X215.539","Y121.681"  ],
  ["G1","X214.187","Y122.634"  ],
  ["G1","X212.770","Y123.355"  ],
  ["G1","X211.302","Y123.896"  ],
  ["G1","X209.023","Y124.501"  ],
  ["G1","X205.971","Y125.171"  ],
  ["G1","X204.464","Y125.557"  ],
  ["G1","X200.228","Y126.767"  ],
  ["G1","X191.742","Y129.098"  ],
  ["G1","X178.981","Y132.459"  ],
  ["G1","X170.469","Y134.687"  ],
  ["G1","X155.995","Y138.460"  ],
  ["G1","X141.534","Y142.233"  ],
  ["G1","X128.644","Y145.645"  ],
  ["G1","X115.586","Y149.122"  ],
  ["G1","X111.646","Y156.269"  ],
  ["G1","X103.765","Y170.588"  ],
  ["G1","X99.773","Y177.722"  ],
  ["G1","X97.005","Y182.693"  ],
  ["G1","X91.571","Y192.685"  ],
  ["G1","X86.175","Y202.678"  ],
  ["G1","X80.664","Y212.632"  ],
  ["G1","X77.818","Y217.551"  ],
  ["G1","X76.775","Y219.367"  ],
  ["G1","X74.727","Y223.011"  ],
  ["G1","X71.779","Y228.535"  ],
  ["G1","X66.074","Y239.713"  ],
  ["G1","X62.249","Y247.143"  ],
  ["G1","X60.408","Y250.452"  ],
  ["G1","X58.258","Y254.174"  ],
  ["G1","X62.340","Y44.212"  ],
  ["G1","X62.468","Y229.282"  ],
  ["G1","X62.533","Y253.259"  ],
  ["G1","X65.520","Y252.397"  ],
  ["G1","X71.482","Y250.594"  ],
  ["G1","X80.380","Y247.709"  ],
  ["G1","X92.189","Y243.756"  ],
  ["G1","X101.061","Y240.846"  ],
  ["G1","X107.010","Y238.992"  ],
  ["G1","X109.998","Y238.103"  ],
  ["G1","X113.938","Y236.944"  ],
  ["G1","X121.793","Y234.510"  ],
  ["G1","X133.524","Y230.712"  ],
  ["G1","X149.118","Y225.509"  ],
  ["G1","X160.824","Y221.646"  ],
  ["G1","X168.653","Y219.161"  ],
  ["G1","X172.593","Y217.950"  ],
  ["G1","X179.650","Y215.774"  ],
  ["G1","X193.712","Y211.267"  ],
  ["G1","X214.740","Y204.288"  ],
  ["G1","X228.763","Y199.652"  ],
  ["G1","X244.873","Y194.437"  ],
  ["G1","X260.969","Y189.209"  ],
  ["G1","X264.072","Y188.114"  ],
  ["G1","X267.073","Y187.007"  ],
  ["G1","X284.946","Y112.783"  ],
  ["G1","X303.000","Y37.761"  ],
  ["G1","X160.540","Y54.359"  ],
  ["G1","X156.793","Y63.476"  ],
  ["G1","X149.221","Y81.504"  ],
  ["G1","X141.701","Y99.468"  ],
  ["G1","X136.190","Y113.040"  ],
  ["G1","X132.623","Y122.183"  ],
  ["G1","X130.884","Y126.793"  ],
  ["G1","X166.812","Y118.397"  ],
  ["G1","X202.816","Y109.989"  ],
  ["G1","X203.898","Y108.778"  ],
  ["G1","X205.868","Y106.550"  ],
  ["G1","X207.375","Y104.954"  ],
  ["G1","X208.160","Y104.155"  ],
  ["G1","X218.758","Y93.789"  ],
  ["G1","X234.674","Y78.259"  ],
  ["G1","X242.748","Y70.623"  ],
  ["G1","X248.221","Y65.640"  ],
  ["G1","X250.989","Y63.180"  ],
  ["G1","X253.346","Y61.081"  ],
  ["G1","X257.969","Y56.806"  ],
  ["G1","X264.768","Y50.252"  ],
  ["G1","X273.743","Y41.354"  ]
]
        for (let index = 0; index < multi_gcode_obj.length; index++) {
          const gcode = multi_gcode_obj[index];
          //console.log(element[0] + " : " + element[1] + " : " + element[2])
          var gcode_construct = gcode[0] + " " + gcode[1] + " " + gcode[2]
          //console.log(gcode_construct)
          this.send_single_gcode(gcode_construct);
          console.log(gcode_construct)
          await new Promise(resolve => setTimeout(resolve, 500));
        }
    },

    /**
     * @description: This function draws the logo of the company on the board.
     * @param {type} none
     * @returns {type} none
     */
    async draw_logo(){
      this.send_single_gcode("G1 X284 Y70 F10000");
      await new Promise(resolve => setTimeout(resolve, 3000)); //Let printer move
      this.turn_on_magnet();
      await new Promise(resolve => setTimeout(resolve, 1000));
      //first shape
      this.send_single_gcode("G1 X284 Y70 F10000");//
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.send_single_gcode("G1 X90 Y133 F10000");//
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.send_single_gcode("G1 X60 Y255 F10000");//
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.send_single_gcode("G1 X130 Y184 F10000");
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.send_single_gcode("G1 X236 Y158 F10000");
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.send_single_gcode("G1 X284 Y70 F10000");
      // await new Promise(resolve => setTimeout(resolve, 1000));
      // this.send_single_gcode("G1 X117 Y180 F10000");
      //second shape
      await new Promise(resolve => setTimeout(resolve, 1500));
      this.turn_off_magnet();
      await new Promise(resolve => setTimeout(resolve, 1500)); //Let printer move
      this.send_single_gcode("G1 X210 Y204 F10000");
      await new Promise(resolve => setTimeout(resolve, 1500));
      this.turn_on_magnet();
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.send_single_gcode("G1 X210 Y204 F10000");
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.send_single_gcode("G1 X154 Y217 F10000");
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.send_single_gcode("G1 X88 Y281 F10000");
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.send_single_gcode("G1 X187 Y259 F10000");
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.send_single_gcode("G1 X210 Y204 F10000");
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.turn_off_magnet();
      // this.send_single_gcode("G1 X248 Y123 F10000");
      // await new Promise(resolve => setTimeout(resolve, 3000)); //Let printer move
      // this.turn_on_magnet();
      // await new Promise(resolve => setTimeout(resolve, 1000));
      // //first shape
      // this.send_single_gcode("G1 X248 Y123 F10000");//
      // await new Promise(resolve => setTimeout(resolve, 1000));
      // this.send_single_gcode("G1 X114 Y167 F10000");//
      // await new Promise(resolve => setTimeout(resolve, 1000));
      // this.send_single_gcode("G1 X95 Y244 F10000");//
      // await new Promise(resolve => setTimeout(resolve, 1000));
      // this.send_single_gcode("G1 X143 Y200 F10000");
      // await new Promise(resolve => setTimeout(resolve, 1000));
      // this.send_single_gcode("G1 X217 Y180 F10000");
      // await new Promise(resolve => setTimeout(resolve, 1000));
      // this.send_single_gcode("G1 X248 Y123 F10000");
      // // await new Promise(resolve => setTimeout(resolve, 1000));
      // // this.send_single_gcode("G1 X117 Y180 F10000");
      // //second shape
      // await new Promise(resolve => setTimeout(resolve, 2000));
      // this.turn_off_magnet();
      // await new Promise(resolve => setTimeout(resolve, 2000)); //Let printer move
      // this.send_single_gcode("G1 X195 Y220 F10000");
      // await new Promise(resolve => setTimeout(resolve, 2000));
      // this.turn_on_magnet();
      // await new Promise(resolve => setTimeout(resolve, 1000));
      // this.send_single_gcode("G1 X195 Y220 F10000");
      // await new Promise(resolve => setTimeout(resolve, 1000));
      // this.send_single_gcode("G1 X161 Y228 F10000");
      // await new Promise(resolve => setTimeout(resolve, 1000));
      // this.send_single_gcode("G1 X120 Y267 F10000");
      // await new Promise(resolve => setTimeout(resolve, 1000));
      // this.send_single_gcode("G1 X181 Y254 F10000");
      // await new Promise(resolve => setTimeout(resolve, 1000));
      // this.send_single_gcode("G1 X195 Y220 F10000");
      // await new Promise(resolve => setTimeout(resolve, 1000));
      // this.turn_off_magnet();

    },

    async demo_moves(itr){
      console.log("Demo Moves")
      //var move_speed = "F5000";
      var short_move_speed = "F10000";
      //var slide_move_speed = "F9000";
      var halfline_offset = 22;
      //var halfline_offset_vertical = 25;

      // 50,  this.mag_toggle_time_slider , this.short_move_time_slider , long_move_time_slider

      console.log(itr)

      // Execute a series of chess moves for two players (White and Black)

      for (let index = 0; index < itr; index++) {
        console.log("Running Itter: " , itr)

        // Move Pawn G6 to G3 for White
await this.AN_move_router({
  "color": "w",
  "from": "g2",
  "to": "g3",
  "flags": "n",
  "piece": "p",
  "san": "g3"
});
this.board_update_tick()

// Move Pawn D7 to D5 for Black
await this.AN_move_router({
  "color": "b",
  "from": "d7",
  "to": "d5",
  "flags": "n",
  "piece": "p",
  "san": "d5"
});

this.board_update_tick()

// Move Knight from G1 to F3 for White
await this.AN_move_router({
  "color": "w",
  "from": "g1",
  "to": "f3",
  "flags": "n",
  "piece": "n",
  "san": "Nf3"
});
this.board_update_tick()

// Move Bishop from C8 to F5 for Black
await this.AN_move_router({
  "color": "b",
  "from": "c8",
  "to": "f5",
  "flags": "n",
  "piece": "b",
  "san": "Bf5"
});
this.board_update_tick()

// Move Pawn D2 to D3 for White
await this.AN_move_router({
  "color": "w",
  "from": "d2",
  "to": "d3",
  "flags": "n",
  "piece": "p",
  "san": "d3"
});
this.board_update_tick()

// Move Knight from B8 to C6 for Black
await this.AN_move_router({
  "color": "b",
  "from": "b8",
  "to": "c6",
  "flags": "n",
  "piece": "n",
  "san": "Nc6"
});
this.board_update_tick()

// Move Bishop from F1 to G2 for White
await this.AN_move_router({
  "color": "w",
  "from": "f1",
  "to": "g2",
  "flags": "n",
  "piece": "b",
  "san": "Bg2"
});
this.board_update_tick()

// Move Pawn E7 to E5 for Black
await this.AN_move_router({
  "color": "b",
  "from": "e7",
  "to": "e5",
  "flags": "n",
  "piece": "p",
  "san": "e5"
});
this.board_update_tick()

// Move Pawn E2 to E4 for White
await this.AN_move_router({
  "color": "w",
  "from": "e2",
  "to": "e4",
  "flags": "n",
  "piece": "p",
  "san": "e4"
});
this.board_update_tick()

// Move Queen from D8 to D6 for Black
await this.AN_move_router({
  "color": "b",
  "from": "d8",
  "to": "d6",
  "flags": "n",
  "piece": "q",
  "san": "Qd6"
});
this.board_update_tick()

// Perform a king-side castle for White (O-O)
await this.AN_move_router({
  "color": "w",
  "from": "e1",
  "to": "g1",
  "flags": "k",
  "piece": "k",
  "san": "O-O"
});
this.board_update_tick()

// Perform a queen-side castle for Black (O-O-O)
await this.AN_move_router({
  "color": "b",
  "from": "e8",
  "to": "c8",
  "flags": "q",
  "piece": "k",
  "san": "O-O-O"
});
this.board_update_tick()

// Reverse the executed chess moves in the opposite order



await this.movement_short_slide(250 , 35 , short_move_speed , this.short_move_time_slider); 
await new Promise(resolve => setTimeout(resolve, 5000));
await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
await this.movement_short_slide(250 + halfline_offset , 35 + halfline_offset , short_move_speed , this.short_move_time_slider);
await this.movement_short_slide(300 + halfline_offset , 35 + halfline_offset , short_move_speed , this.short_move_time_slider);
await this.movement_short_slide(350 , 35 , short_move_speed , this.short_move_time_slider);
await this.movement_mag_toggle_off(this.mag_toggle_time_slider);

await this.movement_short_slide(300 , 35 , short_move_speed , this.short_move_time_slider);
await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
await this.movement_short_slide(200 , 35 , short_move_speed , this.short_move_time_slider);
await this.movement_mag_toggle_off(this.mag_toggle_time_slider);

//Queen Side castle Black
this.board_update_tick()

await this.movement_short_slide(100 , 360 , short_move_speed , this.short_move_time_slider);
await new Promise(resolve => setTimeout(resolve, 5000));
await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
await this.movement_short_slide(100 - halfline_offset , 360 - halfline_offset , short_move_speed , this.short_move_time_slider);
await this.movement_short_slide(0 + halfline_offset , 360 - halfline_offset , short_move_speed , this.short_move_time_slider);
await this.movement_short_slide(0 , 360 , short_move_speed , this.short_move_time_slider);
await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
await this.movement_short_slide(50 , 360 , short_move_speed , this.short_move_time_slider);
await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
await this.movement_short_slide(200 , 360 , short_move_speed , this.short_move_time_slider);
await this.movement_mag_toggle_off(this.mag_toggle_time_slider);

this.board_update_tick()


// Undo Queen-side castle for Black (O-O-O)
// await this.AN_move_router({
//   "color": "b",
//   "from": "c8",
//   "to": "e8",
//   "flags": "q",
//   "piece": "k",
//   "san": "O-O-O"
// });

// // Undo King-side castle for White (O-O)
// await this.AN_move_router({
//   "color": "w",
//   "from": "g1",
//   "to": "e1",
//   "flags": "k",
//   "piece": "k",
//   "san": "O-O"
// });

// Move Pawn E4 to E2 for White
await this.AN_move_router({
  "color": "w",
  "from": "e4",
  "to": "e2",
  "flags": "n",
  "piece": "p",
  "san": "e2"
});
this.board_update_tick()

// Move Queen from D6 to D8 for Black
await this.AN_move_router({
  "color": "b",
  "from": "d6",
  "to": "d8",
  "flags": "n",
  "piece": "q",
  "san": "Qd8"
});
this.board_update_tick()

// Move Bishop from G2 to F1 for White
await this.AN_move_router({
  "color": "w",
  "from": "g2",
  "to": "f1",
  "flags": "n",
  "piece": "b",
  "san": "Bf1"
});
this.board_update_tick()

// Move Pawn from E5 to E7 for Black
await this.AN_move_router({
  "color": "b",
  "from": "e5",
  "to": "e7",
  "flags": "n",
  "piece": "p",
  "san": "e7"
});
this.board_update_tick()

// Move Pawn from D3 to D2 for White
await this.AN_move_router({
  "color": "w",
  "from": "d3",
  "to": "d2",
  "flags": "n",
  "piece": "p",
  "san": "d2"
});
this.board_update_tick()

// Move Knight from C6 to B8 for Black
await this.AN_move_router({
  "color": "b",
  "from": "c6",
  "to": "b8",
  "flags": "n",
  "piece": "n",
  "san": "Nb8"
});
this.board_update_tick()

// Move Pawn from G3 to G2 for White
await this.AN_move_router({
  "color": "w",
  "from": "g3",
  "to": "g2",
  "flags": "n",
  "piece": "p",
  "san": "g2"
});
this.board_update_tick()

// Move Bishop from F5 to C8 for Black
await this.AN_move_router({
  "color": "b",
  "from": "f5",
  "to": "c8",
  "flags": "n",
  "piece": "b",
  "san": "Bc8"
});
this.board_update_tick()

// Move Knight from F3 to G1 for White
await this.AN_move_router({
  "color": "w",
  "from": "f3",
  "to": "g1",
  "flags": "n",
  "piece": "n",
  "san": "Ng1"
});
this.board_update_tick()

// Move Pawn from D5 to D7 for Black
await this.AN_move_router({
  "color": "b",
  "from": "d5",
  "to": "d7",
  "flags": "n",
  "piece": "p",
  "san": "d7"
});
this.board_update_tick()
      }



      console.log("Inner Demo moves")
    },

    /** 
    * @description This function is used to preform the kings felleco chess move
    * @param {number} loop_iterations - The number of times to run the function
    * @param {string} knight_move_type - The type of move to preform with the knight
    * @param {number} mag_toggle_time - The time in ms to wait after turning on or off the magnet
    * @param {number} short_move_time - The time in ms to wait after preforming a short move
    * @param {number} slide_mode_time - The time in ms to wait after preforming a long move
    * @returns {void}
    */
    async kings_felleco(loop_iterations , knight_move_type , mag_toggle_time , short_move_time , slide_mode_time){
      console.log("running kings_felleco" + "|" + knight_move_type + "|" + mag_toggle_time + "|" +short_move_time + "|" +slide_mode_time);
      var move_speed = "F5000";
      var short_move_speed = "F10000";
      var slide_move_speed = "F9000";
      var halfline_offset = 22;
      var halfline_offset_vertical = 25;
      console.log(short_move_speed , slide_move_speed)
      for (let index = 0; index < loop_iterations; index++) {
        console.log("running kings_felleco at index" , index )
        //const element = array[index];
        await this.send_to_cord(300 , 71.43 , move_speed); //Pawn G3 White
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(300 , 117.86 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Pawn D5 Black
        await this.movement_short_slide(150 , 303.57 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(150 , 210.71 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Knight F3 White
        await this.movement_short_slide(300 , 25 , short_move_speed, short_move_time); 
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(300 , 71.43 , short_move_speed , short_move_time);
        await this.movement_short_slide(250 , 117.86 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Bishop f5 Black
        await this.movement_short_slide(100 , 350 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(250 , 210.71 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Pawn D3 White
        await this.movement_short_slide(150 , 71.43 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(150 , 117.86 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Knight c6 Black
        await this.movement_short_slide(50 , 350 , short_move_speed, short_move_time); 
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(50 + halfline_offset_vertical , 350 - halfline_offset , short_move_speed , short_move_time);
        await this.movement_short_slide(50 + halfline_offset_vertical , 257.14 + halfline_offset , short_move_speed , short_move_time);
        await this.movement_short_slide(100 , 257.14 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

         //Bishop G2
        await this.movement_short_slide(250 , 25 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(300 , 71.43 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Pawn e5 Black
        await this.movement_short_slide(200 , 303.57 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(200 , 210.71 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Pawn E4 White
        await this.movement_short_slide(200 , 71.43 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(200 , 164.29 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Queen d6 Black
        await this.movement_short_slide(150 , 350 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(150 , 257.14 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //King side Castle White
        await this.movement_short_slide(200 , 25 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(300 , 25 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        await this.movement_short_slide(350 , 25 , short_move_speed , short_move_time); 
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(300 + halfline_offset , 25 + halfline_offset , short_move_speed , short_move_time);
        await this.movement_short_slide(250 + halfline_offset , 25 + halfline_offset , short_move_speed , short_move_time);
        await this.movement_short_slide(250 , 25 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Queen Side castle Black
        await this.movement_short_slide(200 , 350 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(50 , 350 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        await this.movement_short_slide(0 , 350 , short_move_speed , short_move_time); 
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(0 + halfline_offset , 350 - halfline_offset , short_move_speed , short_move_time);
        await this.movement_short_slide(100 - halfline_offset , 350 - halfline_offset , short_move_speed , short_move_time);
        await this.movement_short_slide(100 , 350 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);
        
        //Reverse Position
        ////////////////////////////////////////////////////////////////
        //King side Castle White
      

        await this.movement_short_slide(250 , 25 , short_move_speed , short_move_time); 
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(250 + halfline_offset , 25 + halfline_offset , short_move_speed , short_move_time);
        await this.movement_short_slide(300 + halfline_offset , 25 + halfline_offset , short_move_speed , short_move_time);
        await this.movement_short_slide(350 , 25 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        await this.movement_short_slide(300 , 25 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(200 , 25 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Queen Side castle Black

        
        await this.movement_short_slide(100 , 350 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(100 - halfline_offset , 350 - halfline_offset , short_move_speed , short_move_time);
        await this.movement_short_slide(0 + halfline_offset , 350 - halfline_offset , short_move_speed , short_move_time);
        await this.movement_short_slide(0 , 350 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);
        await this.movement_short_slide(50 , 350 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(200 , 350 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Pawn E4 White
        
        await this.movement_short_slide(200 , 164.29 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(200 , 71.43 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Queen d6 Black
       
        await this.movement_short_slide(150 , 257.14 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(150 , 350 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Bishop G2 White
        await this.movement_short_slide(300 , 71.43 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(250 , 25 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Pawn e5 Black
        
        await this.movement_short_slide(200 , 210.71 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(200 , 303.57 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Pawn D3 White
        
        await this.movement_short_slide(150 , 117.86 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(150 , 71.43 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Knight c6 Black
        await this.movement_short_slide(100 , 257.14 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(50 + halfline_offset_vertical , 257.14 + halfline_offset , short_move_speed , short_move_time);
        await this.movement_short_slide(50 + halfline_offset_vertical , 350 - halfline_offset , short_move_speed , short_move_time);
        await this.movement_short_slide(50 , 350 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Knight F3 White
        await this.movement_short_slide(250 , 117.86 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(300 , 71.43 , short_move_speed , short_move_time);
        await this.movement_short_slide(300 , 25 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Bishop f5 Black
        
        await this.movement_short_slide(250 , 210.71 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(100 , 350 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Pawn G3 White
        
        await this.movement_short_slide(300 , 117.86 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(300 , 71.43 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);

        //Pawn D5 Black
        
        await this.movement_short_slide(150 , 210.71 , short_move_speed , short_move_time);
        await this.movement_mag_toggle_on(mag_toggle_time);
        await this.movement_short_slide(150 , 303.57 , short_move_speed, short_move_time);
        await this.movement_mag_toggle_off(mag_toggle_time);
        //////

        // this.movement_mag_toggle_off(mag_toggle_time);
        // this.movement_mag_toggle_on(mag_toggle_time);
        // this.movement_short_slide(0 , 0 , short_move_speed , short_move_time);
        // this.movement_long_slide(350 , 350 , slide_move_speed , slide_mode_time);
        // this.turn_off_magnet();
        // await new Promise(resolve => setTimeout(resolve, mag_toggle_time));

        // this.turn_on_magnet();
        // await new Promise(resolve => setTimeout(resolve, mag_toggle_time));

        // this.send_single_gcode("G1 X Y" + short_move_speed); //short move
        // await new Promise(resolve => setTimeout(resolve, short_move_time));

        // this.send_single_gcode("G1 X Y" + slide_move_speed); //long move
        // await new Promise(resolve => setTimeout(resolve, slide_mode_time));
      }
    },

    /**
     * @description: This function sends the gcode to the printer to move to a specific x and y cordinate at a specific speed
     * @param {number} x_cord - The x cordinate to move to
     * @param {number} y_cord - The y cordinate to move to
     * @param {number} move_speed - The speed at which the printer will move
     */
    async send_to_cord(x_cord , y_cord , move_speed){
      this.send_single_gcode("G1 X" + x_cord + " Y" + y_cord + move_speed);
        await new Promise(resolve => setTimeout(resolve, 5000));
    },

    /**
     * @description: This function is used to turn off the magnet for a specified amount of time.
     * @param {number} mag_toggle_time - The amount of time in milliseconds that the magnet will be turned off for.
     */
    async movement_mag_toggle_off(mag_toggle_time){
      this.turn_off_magnet();
        await new Promise(resolve => setTimeout(resolve, mag_toggle_time));
    },

    /**
     * @description: This function turns on the magnet for a specified amount of time.
     * @param {number} mag_toggle_time - The amount of time in milliseconds that the magnet will be turned on.
     */
    async movement_mag_toggle_on(mag_toggle_time){
      this.turn_on_magnet();
        await new Promise(resolve => setTimeout(resolve, mag_toggle_time));
    },

    /**
     * @description: This function preforms a short slide movement to the specified x and y coordinates.
     * @param {number} x_cord - The x coordinate to move to.
     * @param {number} y_cord - The y coordinate to move to.
     * @param {string} short_move_speed - The speed of the short slide movement.
     * @param {number} short_move_time - The time in milliseconds for the short slide movement.
     */
    async movement_short_slide(x_cord , y_cord , short_move_speed , short_move_time){
      console.log("G1 X" + x_cord + " Y" + y_cord + short_move_speed)
      this.send_single_gcode("G1 X" + x_cord + " Y" + y_cord + short_move_speed); //short move
        await new Promise(resolve => setTimeout(resolve, short_move_time));
    },

    /**
     * @description: This function preforms a long slide movement to the given x and y coordinates.
     * @param {number} x_cord - The x coordinate to move to.
     * @param {number} y_cord - The y coordinate to move to.
     * @param {string} slide_move_speed - The speed at which the machine will move at.
     * @param {number} slide_mode_time - The time in milliseconds that the machine will stay in slide mode for.
     */
    async movement_long_slide(x_cord , y_cord , slide_move_speed , slide_mode_time){
      this.send_single_gcode("G1 X"+ x_cord + " Y" + y_cord + slide_move_speed); //long move
        await new Promise(resolve => setTimeout(resolve, slide_mode_time));
    },

    /**
     * @description: This function is used to recenter the pieces on the board.
     * @param {number} mag_toggle_time - The time it takes for the magnet to toggle on or off.
     * @param {number} short_move_time - The time it takes for the robot to move a short distance.
     * @param {number} slide_mode_time - The time it takes for the robot to move in slide mode.
     */
    async recenter_pieces( mag_toggle_time , short_move_time , slide_mode_time){
      var short_move_time_override = 2500;
      await this.movement_mag_toggle_off(mag_toggle_time);
      for (let index = 0; index < this.cord_map.length; index++) {
        const cord_map_in = this.cord_map[index];
        if(cord_map_in.real_y < 3 || cord_map_in.real_y > 6){
          await new Promise(resolve => setTimeout(resolve, short_move_time_override));
          await this.relative_AN_move(cord_map_in.chess_cord , mag_toggle_time , short_move_time_override , slide_mode_time);
          await this.movement_mag_toggle_on(mag_toggle_time);
          await this.movement_mag_toggle_off(mag_toggle_time);
        }
        //console.log(cord_map_in);
        
      }
    },

    /**
     * @description: This function is the router for all the relative move functions. It takes in a piece_move_object and routes it to the correct function based on the piece type.
     * @param {piece_move_object} piece_move_object - The object that contains all the information about the move.
     */
    async AN_move_router(piece_move_object){
      //console.log("Running AN_move_router: "  + san + orig + dest + color + "|" + piece);
      console.log("Piece move object")
      console.log(piece_move_object)
      if (piece_move_object.san.includes("x")){
        await this.relative_capture(piece_move_object);
        return
      }
      switch (piece_move_object.piece) {
        case "p":
            console.log("send_pawn");
            await this.relative_pawn_move(piece_move_object);
          break;
        case "n":
            console.log("send_knight");
            await this.relative_knigh_move(piece_move_object);
          break;
        case "b":
            console.log("send_bishop");
            await this.relative_bishop_move(piece_move_object);
          break;
        case "r":
            console.log("send_rook");
            await this.relative_rook_move(piece_move_object);
          break;
        case "q":
            console.log("send_queen");
            await this.relative_queen_move(piece_move_object);
          break;
        case "k":
            console.log("send_king");
            if (piece_move_object.san.includes("O-O")){
              console.log('Castling King Side')
              await this.relative_castle_move(piece_move_object);
            }else if (piece_move_object.san.includes("O-O-O")){
              console.log('Castling Queen Side')
              await this.relative_castle_move(piece_move_object);
            }else{
              await this.relative_king_move(piece_move_object);
            }
          break;
        default:
          break;
      }
    },

    find_middle_line_in(cord_map_in) {
      //find which line in-between
      switch (cord_map_in.real_x) {
        case 1:
          this.current_move_in_line_vert = 1
          break;
        case 2:
          this.current_move_in_line_vert = 2
          break;
        case 3:
          this.current_move_in_line_vert = 3
          break;
        case 4:
          this.current_move_in_line_vert = 4
          break;
        case 5:
          this.current_move_in_line_vert = 5
          break;
        case 6:
          this.current_move_in_line_vert = 6
          break;
        case 7:
          this.current_move_in_line_vert = 7
          break;
        case 8:
          this.current_move_in_line_vert = 7
          break;
        default:
          break;
      }
      switch (cord_map_in.real_y) {
        case 1:
          this.current_move_in_line_horz = 1
          break;
        case 2:
          this.current_move_in_line_horz = 2
          break;
        case 3:
          this.current_move_in_line_horz = 3
          break;
        case 4:
          this.current_move_in_line_horz = 4
          break;
        case 5:
          this.current_move_in_line_horz = 5
          break;
        case 6:
          this.current_move_in_line_horz = 6
          break;
        case 7:
          this.current_move_in_line_horz = 7
          break;
        case 8:
          this.current_move_in_line_horz = 7
          break;
        default:
          break;
      }
      // {
      //     "chess_cord": "a1",
      //     "real_x": 1,
      //     "real_y": 1,
      //     "send_gcode": {
      //       "gcode": "G1 X0 Y25 F6000",
      //       "out_val_x": 0,
      //       "out_val_y": 25
      //     }
      //   },
    },

    find_middle_line_out(cord_map_in) {
      //find which line in-between
      switch (cord_map_in.real_x) {
        case 1:
          this.current_move_out_line_vert = 1
          break;
        case 2:
          this.current_move_out_line_vert = 2
          break;
        case 3:
          this.current_move_out_line_vert = 3
          break;
        case 4:
          this.current_move_out_line_vert = 4
          break;
        case 5:
          this.current_move_out_line_vert = 5
          break;
        case 6:
          this.current_move_out_line_vert = 6
          break;
        case 7:
          this.current_move_out_line_vert = 7
          break;
        case 8:
          this.current_move_out_line_vert = 7
          break;
        default:
          break;
      }
      switch (cord_map_in.real_y) {
        case 1:
          this.current_move_out_line_horz = 1
          break;
        case 2:
          this.current_move_out_line_horz = 2
          break;
        case 3:
          this.current_move_out_line_horz = 3
          break;
        case 4:
          this.current_move_out_line_horz = 4
          break;
        case 5:
          this.current_move_out_line_horz = 5
          break;
        case 6:
          this.current_move_out_line_horz = 6
          break;
        case 7:
          this.current_move_out_line_horz = 7
          break;
        case 8:
          this.current_move_out_line_horz = 7
          break;
        default:
          break;
      }
      // {
      //     "chess_cord": "a1",
      //     "real_x": 1,
      //     "real_y": 1,
      //     "send_gcode": {
      //       "gcode": "G1 X0 Y25 F6000",
      //       "out_val_x": 0,
      //       "out_val_y": 25
      //     }
      //   },
    },

    /**
     * @description This function preforms a relative move of a pawn piece
     * @param {object} piece_move_object
     * @returns {Promise<void>}
     */
    async relative_pawn_move(piece_move_object){
    //   this.mag_toggle_time_slider = 2560
    // this.short_move_time_slider = 500
    // this.long_move_time_slider = 2300
    
      console.log('running relative_pawn_move |' + piece_move_object.san); //to opease the list gods
      
      for (let index = 0; index < this.cord_map.length; index++) {
        const cord_map_in = this.cord_map[index];
        if(cord_map_in.chess_cord === piece_move_object.from){
          //console.log(cord_map_in.chess_cord)
          this.move_start = cord_map_in.chess_cord;
        }
        if(cord_map_in.chess_cord === piece_move_object.to){
          //console.log(cord_map_in.chess_cord)
          this.move_end = cord_map_in.chess_cord;
        }
      }

      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      await this.relative_AN_move(this.move_start , this.mag_toggle_time_slider , this.short_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1500));
      await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
      await this.relative_AN_move(this.move_end , this.mag_toggle_time_slider , this.short_move_time_slider , this.long_move_time_slider);
      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      
    },

    async relative_capture(piece_move_object){
    //   this.mag_toggle_time_slider = 2560
    // this.short_move_time_slider = 500
    // this.long_move_time_slider = 2300
    
      console.log('running relative_capture |' + piece_move_object.san); //to opease the list gods

      //Find middle line

      //Find to piece

      //Move piece to non outside

      //move piece to centerline

      //move piece to edge

      //Handle Removal Later

      //Go back to first piece and move to end
      
      var short_move_speed = "F10000";
      // var halfline_offset = 22;
      // var halfline_offset_vertical = 25;
    
      //console.log('running relative_knigh_move |' + piece_move_object.san); //to opease the list gods
      
      for (let index = 0; index < this.cord_map.length; index++) {
        const cord_map_in = this.cord_map[index];
        if(cord_map_in.chess_cord === piece_move_object.to){
          console.log(cord_map_in.chess_cord)
          this.find_middle_line_in(cord_map_in);
          this.move_start = cord_map_in.chess_cord;
          this.move_start_obj = cord_map_in
          //Find dirction to middle line
          if(this.move_start_obj.real_y < 4){
            //move up
            this.move_end_obj = {'chess_cord': null, 'real_x': this.move_start_obj.real_x, 'real_y': this.move_start_obj.real_y, 'send_gcode': {
                'gcode': this.move_start_obj.send_gcode.gcode ,
                'out_val_x': this.move_start_obj.send_gcode.out_val_x ,
                'out_val_y': 187.5 + this.offset_y_board_length  // +- 23.2142857143
              }}
          }else{
            //move down
            this.move_end_obj = {'chess_cord': null, 'real_x': this.move_start_obj.real_x, 'real_y': this.move_start_obj.real_y, 'send_gcode': {
                'gcode': this.move_start_obj.send_gcode.gcode ,
                'out_val_x': this.move_start_obj.send_gcode.out_val_x ,
                'out_val_y': 187.5 + this.offset_y_board_length
              }}
          }
          this.move_end = cord_map_in.chess_cord;
        }
        // if(cord_map_in.chess_cord === piece_move_object.to){
        //   //console.log(cord_map_in.chess_cord)
        //   this.find_middle_line_out(cord_map_in);
        //   this.move_end = cord_map_in.chess_cord;
        //   this.move_end_obj = cord_map_in
        //   //console.log();
        // }
      }

      console.log(this.move_start_obj);
      console.log(this.move_end_obj); 
      console.log(this.current_move_in_line_vert + "|" + this.current_move_in_line_horz + "|" +this.current_move_out_line_vert + "|" + this.current_move_out_line_horz )

      var halfline_offset = 22;
      //var halfline_offset_vertical = 25;

      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      await this.relative_AN_move(this.move_start , this.mag_toggle_time_slider , this.short_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1500)); 
      await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
      //map remove direction

      // console.log(this.move_start_obj < 8)
      // console.log(this.move_start_obj)

      //console.log("Capturing Piece with params: " , this.move_start_obj.real_y)

      if(this.move_start_obj.real_y <= 4){
        if(this.move_start_obj.real_x <= 4){
          console.log("capture from quad a1")
          await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x + halfline_offset , this.move_end_obj.send_gcode.out_val_y , short_move_speed , this.short_move_time_slider);
        }else{
          console.log("capture from quad h1")
          await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x - halfline_offset , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset , this.move_end_obj.send_gcode.out_val_y , short_move_speed , this.short_move_time_slider);
        }
      }else{
        if(this.move_start_obj.real_x <= 4){
          console.log("capture from quad a8")
          await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset , this.move_start_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x + halfline_offset , this.move_end_obj.send_gcode.out_val_y , short_move_speed , this.short_move_time_slider);
        }else{
          console.log("capture from quad h8")
          await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x - halfline_offset , this.move_start_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset , this.move_end_obj.send_gcode.out_val_y , short_move_speed , this.short_move_time_slider);
        }
        // await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x - halfline_offset , this.move_start_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset , this.move_end_obj.send_gcode.out_val_y , short_move_speed , this.short_move_time_slider);
      }

      //move off board
      //Move Off center
      if(piece_move_object.color == "w"){
        await this.movement_long_slide(0 , this.move_end_obj.send_gcode.out_val_y , short_move_speed , this.long_move_time_slider);
        await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
        await this.movement_long_slide(0 + this.magnet_launch_offset , this.move_end_obj.send_gcode.out_val_y , short_move_speed , this.long_move_time_slider);
        await this.toggle_magnet_polarity();
        await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
        await this.toggle_magnet_polarity();
        await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      }else{
        await this.movement_long_slide(350 , this.move_end_obj.send_gcode.out_val_y , short_move_speed , this.long_move_time_slider);
        await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
        await this.movement_long_slide(350 - this.magnet_launch_offset , this.move_end_obj.send_gcode.out_val_y , short_move_speed , this.long_move_time_slider);
        await this.toggle_magnet_polarity();
        await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
        await this.toggle_magnet_polarity();
        await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      }


      var piece_move_object_strip_san = {
        "color": piece_move_object.color,
        "from": piece_move_object.from,
        "to": piece_move_object.to,
        "flags": piece_move_object.flags,
        "piece": piece_move_object.piece,
        "captured": piece_move_object.captured,
        "san": "null"
      };
      await this.AN_move_router(piece_move_object_strip_san);
      
    },

    async strip_san_finish_capture(piece_move_object){
      var piece_move_object_strip_san = {
        "color": piece_move_object.color,
        "from": piece_move_object.from,
        "to": piece_move_object.to,
        "flags": piece_move_object.flags,
        "piece": piece_move_object.piece,
        "captured": piece_move_object.captured,
        "san": "null"
      };
      await new Promise(resolve => setTimeout(resolve, 1500)); 
      await this.AN_move_router(piece_move_object_strip_san);
    },

    /**
     * @description This function draws a square marker on the board.
     * @param {number} mag_toggle_time_slider - The time it takes to toggle the magnet.
     * @param {number} long_move_time_slider - The time it takes to move the piece.
     */
    async draw_square_marker(){
      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      await this.relative_AN_move("a1" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 2500));
      await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
      await this.relative_AN_move("a8" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("b8" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("b1" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("c1" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("c8" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("d8" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("d1" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("e1" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("e8" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("f8" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("f1" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("g1" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("g8" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("h8" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("h1" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));

      await this.relative_AN_move("a1" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("a2" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("h2" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("h3" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("a3" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("a4" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("h4" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("h5" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("a5" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("a6" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("h6" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("h7" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("a7" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("a8" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.relative_AN_move("h8" , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
    },

    /**
     * @description: This function is used to move the knight piece on the chess board.
     * @param {object} piece_move_object - The object that contains the information about the move.
     * @returns {void}
     */
    async relative_knigh_move(piece_move_object){
    //   this.mag_toggle_time_slider = 2560
    // this.short_move_time_slider = 500
    // this.long_move_time_slider = 2300
      //var move_speed = "F5000";
      //var slide_move_speed = "F9000";

      var short_move_speed = "F10000";
      var halfline_offset = 22;
      var halfline_offset_vertical = 25;
    
      console.log('running relative_knigh_move |' + piece_move_object.san); //to opease the list gods
      
      for (let index = 0; index < this.cord_map.length; index++) {
        const cord_map_in = this.cord_map[index];
        if(cord_map_in.chess_cord === piece_move_object.from){
          //console.log(cord_map_in.chess_cord)
          this.find_middle_line_in(cord_map_in);
          this.move_start = cord_map_in.chess_cord;
          this.move_start_obj = cord_map_in
        }
        if(cord_map_in.chess_cord === piece_move_object.to){
          //console.log(cord_map_in.chess_cord)
          this.find_middle_line_out(cord_map_in);
          this.move_end = cord_map_in.chess_cord;
          this.move_end_obj = cord_map_in
        }
      }

      console.log(this.current_move_in_line_vert + "|" + this.current_move_in_line_horz + "|" +this.current_move_out_line_vert + "|" + this.current_move_out_line_horz )


      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      await this.relative_AN_move(this.move_start , this.mag_toggle_time_slider , this.short_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1500)); 
      await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
      //map knight direction
      if(this.current_move_in_line_vert > this.current_move_out_line_vert && this.current_move_in_line_horz > this.current_move_out_line_horz){
        console.log("Knight is moving to index 1")
        await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        // if(this.current_move_in_line_horz == this.current_move_out_line_horz + 2 ){
        //   console.log("bot_left")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        // }else{
        //   console.log("left_bot")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        // }
      }
      if(this.current_move_in_line_vert > this.current_move_out_line_vert && this.current_move_in_line_horz < this.current_move_out_line_horz){
        console.log("Knight is moving to index 2")
          await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // if(this.current_move_in_line_horz == this.current_move_out_line_horz - 2 ){
        //   console.log("top_left")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // }else{
        //   console.log("left_top")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // }
      }
      if(this.current_move_in_line_vert < this.current_move_out_line_vert && this.current_move_in_line_horz > this.current_move_out_line_horz){
        console.log("Knight is moving to index 3")
          await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider); 
        // if(this.current_move_in_line_horz == this.current_move_out_line_horz + 2 ){
        //   console.log("bot_right")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        // }else{
        //   console.log("right_bot")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        // }
      }
      if(this.current_move_in_line_vert < this.current_move_out_line_vert && this.current_move_in_line_horz < this.current_move_out_line_horz){
        console.log("Knight is moving to index 4")
        await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // if(this.current_move_in_line_horz == this.current_move_out_line_horz - 2 ){
        //   console.log("top_right")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // }else{
        //   console.log("right_top")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // }
      }
      
      if(this.current_move_in_line_vert == this.current_move_out_line_vert && this.current_move_in_line_horz == this.current_move_out_line_horz){
        console.log("Knight is moving to index 3 edge")
          await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider); 
        // if(this.current_move_in_line_horz == this.current_move_out_line_horz + 2 ){
        //   console.log("bot_right")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        // }else{
        //   console.log("right_bot")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        // }
      }
      if(this.current_move_in_line_vert < this.current_move_out_line_vert && this.current_move_in_line_horz == this.current_move_out_line_horz){
        console.log("Knight is moving to index 2 edge pos")
        await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // if(this.current_move_in_line_horz == this.current_move_out_line_horz - 2 ){
        //   console.log("top_right")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // }else{
        //   console.log("right_top")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // }
      }

      if(this.current_move_in_line_vert < this.current_move_out_line_vert && this.current_move_in_line_horz == this.current_move_out_line_horz){
        console.log("Knight is moving to index 2 edge neg")
        await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // if(this.current_move_in_line_horz == this.current_move_out_line_horz - 2 ){
        //   console.log("top_right")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // }else{
        //   console.log("right_top")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // }
      }

      if(this.current_move_in_line_vert == this.current_move_out_line_vert && this.current_move_in_line_horz < this.current_move_out_line_horz){
        console.log("Knight is moving to index 4 edge pos")
          await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // if(this.current_move_in_line_horz == this.current_move_out_line_horz - 2 ){
        //   console.log("top_left")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // }else{
        //   console.log("left_top")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // }
      }

      if(this.current_move_in_line_vert == this.current_move_out_line_vert && this.current_move_in_line_horz > this.current_move_out_line_horz){
        console.log("Knight is moving to index 4 edge neg")
          await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        // if(this.current_move_in_line_horz == this.current_move_out_line_horz - 2 ){
        //   console.log("top_left")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // }else{
        //   console.log("left_top")
        //   await this.movement_short_slide(this.move_start_obj.send_gcode.out_val_x - halfline_offset_vertical , this.move_start_obj.send_gcode.out_val_y + halfline_offset , short_move_speed , this.short_move_time_slider);
        //   await this.movement_short_slide(this.move_end_obj.send_gcode.out_val_x + halfline_offset_vertical , this.move_end_obj.send_gcode.out_val_y - halfline_offset , short_move_speed , this.short_move_time_slider);
        // }
      }
   
      await this.relative_AN_move(this.move_end , this.mag_toggle_time_slider , this.short_move_time_slider , this.long_move_time_slider);
      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      
    },
    
    /**
     * @description: This function is used to move the bishop piece on the chess board.
     * @param {object} piece_move_object - The object that contains the information about the move.
     * @returns {void}
     */
    async relative_bishop_move(piece_move_object){
    //   this.mag_toggle_time_slider = 2560
    // this.short_move_time_slider = 500
    // this.long_move_time_slider = 2300
    
      console.log('running relative_bishop_move |' + piece_move_object.san); //to opease the list gods
      
      for (let index = 0; index < this.cord_map.length; index++) {
        const cord_map_in = this.cord_map[index];
        if(cord_map_in.chess_cord === piece_move_object.from){
          //console.log(cord_map_in.chess_cord)
          this.move_start = cord_map_in.chess_cord;
        }
        if(cord_map_in.chess_cord === piece_move_object.to){
          //console.log(cord_map_in.chess_cord)
          this.move_end = cord_map_in.chess_cord;
        }
      }

      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      await this.relative_AN_move(this.move_start , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1500));
      await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
      await this.relative_AN_move(this.move_end , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      
    },

    /**
     * @description 
     * @param {string} piece_move_object.san - The move in SAN notation.
     * @param {string} piece_move_object.from - The square the piece is moving from (in algebraic notation).
     * @param {string} piece_move_object.to - The square the piece is moving to (in algebraic notation).
     * @param {string} [piece_move_object.flags] - Any flags or special properties of this move. See below for details on each flag.
     * @param {string} [piece_move_object.piece] - The type of piece making the move (if not specified, defaults to the moving piece type in Game#turn).
     * @param {string} [piece_move_object.color] - The color of the piece making the move (if not specified, defaults to the moving color in Game#turn).
     * @param {string} [piece_move_object.san] - The move in SAN notation (if not specified, will be generated).
     */
    async relative_rook_move(piece_move_object){
    //   this.mag_toggle_time_slider = 2560
    // this.short_move_time_slider = 500
    // this.long_move_time_slider = 2300
    
      console.log('running relative_rook_move |' + piece_move_object.san); //to opease the list gods
      
      for (let index = 0; index < this.cord_map.length; index++) {
        const cord_map_in = this.cord_map[index];
        if(cord_map_in.chess_cord === piece_move_object.from){
          //console.log(cord_map_in.chess_cord)
          this.move_start = cord_map_in.chess_cord;
        }
        if(cord_map_in.chess_cord === piece_move_object.to){
          //console.log(cord_map_in.chess_cord)
          this.move_end = cord_map_in.chess_cord;
        }
      }

      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      await this.relative_AN_move(this.move_start , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1500));
      await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
      await this.relative_AN_move(this.move_end , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      
    },
    /**
     * @description This function is used to move the queen piece on the chess board.
     * @param {object} piece_move_object - The object that contains the information about the move.
     */
    async relative_queen_move(piece_move_object){
    //   this.mag_toggle_time_slider = 2560
    // this.short_move_time_slider = 500
    // this.long_move_time_slider = 2300
    
      console.log('running relative_queen_move |' + piece_move_object.san); //to opease the list gods
      
      for (let index = 0; index < this.cord_map.length; index++) {
        const cord_map_in = this.cord_map[index];
        if(cord_map_in.chess_cord === piece_move_object.from){
          //console.log(cord_map_in.chess_cord)
          this.move_start = cord_map_in.chess_cord;
        }
        if(cord_map_in.chess_cord === piece_move_object.to){
          //console.log(cord_map_in.chess_cord)
          this.move_end = cord_map_in.chess_cord;
        }
      }

      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      await this.relative_AN_move(this.move_start , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1500));
      await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
      await this.relative_AN_move(this.move_end , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1000));
      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      
    },

    /**
     * @description: This function is used to move the king piece in a relative manner.
     * @param {object} piece_move_object - The object containing the chess move information.
     * @returns {void}
     */
    async relative_king_move(piece_move_object){
    //   this.mag_toggle_time_slider = 2560
    // this.short_move_time_slider = 500
    // this.long_move_time_slider = 2300
    
      console.log('running relative_king_move |' + piece_move_object.san); //to opease the list gods
      
      for (let index = 0; index < this.cord_map.length; index++) {
        const cord_map_in = this.cord_map[index];
        if(cord_map_in.chess_cord === piece_move_object.from){
          //console.log(cord_map_in.chess_cord)
          this.move_start = cord_map_in.chess_cord;
        }
        if(cord_map_in.chess_cord === piece_move_object.to){
          //console.log(cord_map_in.chess_cord)
          this.move_end = cord_map_in.chess_cord;
        }
      }

      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      await this.relative_AN_move(this.move_start , this.mag_toggle_time_slider , this.short_move_time_slider , this.long_move_time_slider);
      await new Promise(resolve => setTimeout(resolve, 1500));
      await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
      await this.relative_AN_move(this.move_end , this.mag_toggle_time_slider , this.short_move_time_slider , this.long_move_time_slider);
      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      
    },

    /**
     * @description: This function is used to move the castle piece on the chess board.
     * @param {object} piece_move_object - The object that contains the information about the move.
     * @returns {void}
     */
    async relative_castle_move(piece_move_object){

      var short_move_speed = "F10000";
      //var halfline_offset = 22;
      var halfline_offset_vertical = 25;

          
      console.log('running relative_castle_move |' + piece_move_object.san); //to opease the list gods
      
      for (let index = 0; index < this.cord_map.length; index++) {
        const cord_map_in = this.cord_map[index];
        if(cord_map_in.chess_cord === piece_move_object.from){
          //console.log(cord_map_in.chess_cord)
          this.move_start = cord_map_in.chess_cord;
        }
        if(cord_map_in.chess_cord === piece_move_object.to){
          //console.log(cord_map_in.chess_cord)
          this.move_end = cord_map_in.chess_cord;
        }
      }

      if(piece_move_object.color == "w"){
        console.log("white castle");
        if(piece_move_object.san == "O-O"){
          console.log("King Side")
          await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
          await this.movement_short_slide(200 , 25 + this.offset_y_board_length , short_move_speed , this.short_move_time_slider);
          await new Promise(resolve => setTimeout(resolve, 1500)); 
          
          await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
          await this.movement_short_slide(300 , 25 + this.offset_y_board_length , short_move_speed , this.short_move_time_slider);
          await this.movement_mag_toggle_off(this.mag_toggle_time_slider);

          await this.movement_short_slide(350 , 25 + this.offset_y_board_length , short_move_speed , this.short_move_time_slider); 
          await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
          await this.movement_short_slide(300 + halfline_offset_vertical , 25 + this.offset_y_board_length + halfline_offset_vertical , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(250 + halfline_offset_vertical , 25 + this.offset_y_board_length + halfline_offset_vertical , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(250 , 25 + this.offset_y_board_length , short_move_speed , this.short_move_time_slider);
          await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
        }else{
          console.log("Queen Side")
          await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
          await this.movement_short_slide(200 , 25 + this.offset_y_board_length , short_move_speed , this.short_move_time_slider);
          await new Promise(resolve => setTimeout(resolve, 1500)); 

          await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
          await this.movement_short_slide(100 , 25 + this.offset_y_board_length , short_move_speed , this.short_move_time_slider);
          await this.movement_mag_toggle_off(this.mag_toggle_time_slider);

          await this.movement_short_slide(0 , 25 + this.offset_y_board_length , short_move_speed , this.short_move_time_slider); 
          await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
          await this.movement_short_slide(0 + halfline_offset_vertical , 25 + this.offset_y_board_length + halfline_offset_vertical , short_move_speed , this.short_move_time_slider);
          await this.movement_long_slide(150 - halfline_offset_vertical , 25 + this.offset_y_board_length + halfline_offset_vertical , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(150 , 25 + this.offset_y_board_length , short_move_speed , this.short_move_time_slider);
          await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
        }
      }else{
        console.log("black castle")
        if(piece_move_object.san == "O-O"){
          console.log("King Side")
          await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
          await this.movement_short_slide(200 , 360 , short_move_speed , this.short_move_time_slider);
          await new Promise(resolve => setTimeout(resolve, 1500)); 

          await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
          await this.movement_short_slide(300 , 360 , short_move_speed , this.short_move_time_slider);
          await this.movement_mag_toggle_off(this.mag_toggle_time_slider);

          await this.movement_short_slide(350 , 360 , short_move_speed , this.short_move_time_slider); 
          await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
          await this.movement_short_slide(300 + halfline_offset_vertical , 360 - halfline_offset_vertical , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(250 + halfline_offset_vertical , 360 - halfline_offset_vertical , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(250 , 360 , short_move_speed , this.short_move_time_slider);
          await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
        }else{
          console.log("Queen Side")
          await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
          await this.movement_short_slide(200 , 360 , short_move_speed , this.short_move_time_slider);
          await new Promise(resolve => setTimeout(resolve, 1500)); 

          await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
          await this.movement_short_slide(100 , 360 , short_move_speed , this.short_move_time_slider);
          await this.movement_mag_toggle_off(this.mag_toggle_time_slider);

          await this.movement_short_slide(0 , 360 , short_move_speed , this.short_move_time_slider); 
          await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
          await this.movement_short_slide(0 + halfline_offset_vertical , 360 - halfline_offset_vertical , short_move_speed , this.short_move_time_slider);
          await this.movement_long_slide(150 - halfline_offset_vertical , 360 - halfline_offset_vertical , short_move_speed , this.short_move_time_slider);
          await this.movement_short_slide(150 , 360 , short_move_speed , this.short_move_time_slider);
          await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
        }
      }

      // await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      // await this.relative_AN_move(this.move_start , this.mag_toggle_time_slider , this.short_move_time_slider , this.long_move_time_slider);
      // await new Promise(resolve => setTimeout(resolve, 1500));
      // await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
      // await this.relative_AN_move(this.move_end , this.mag_toggle_time_slider , this.short_move_time_slider , this.long_move_time_slider);
      // await this.movement_mag_toggle_off(this.mag_toggle_time_slider);

      // //King side Castle White
      // await this.movement_short_slide(200 , 25 , short_move_speed , short_move_time);
      // await this.movement_mag_toggle_on(mag_toggle_time);
      // await this.movement_short_slide(300 , 25 , short_move_speed , short_move_time);
      // await this.movement_mag_toggle_off(mag_toggle_time);

      // await this.movement_short_slide(350 , 25 , short_move_speed , short_move_time); 
      // await this.movement_mag_toggle_on(mag_toggle_time);
      // await this.movement_short_slide(300 + halfline_offset , 25 + halfline_offset , short_move_speed , short_move_time);
      // await this.movement_short_slide(250 + halfline_offset , 25 + halfline_offset , short_move_speed , short_move_time);
      // await this.movement_short_slide(250 , 25 , short_move_speed , short_move_time);
      // await this.movement_mag_toggle_off(mag_toggle_time);

      // //Queen Side castle Black
      // await this.movement_short_slide(200 , 350 , short_move_speed , short_move_time);
      // await this.movement_mag_toggle_on(mag_toggle_time);
      // await this.movement_short_slide(50 , 350 , short_move_speed , short_move_time);
      // await this.movement_mag_toggle_off(mag_toggle_time);

      // await this.movement_short_slide(0 , 350 , short_move_speed , short_move_time); 
      // await this.movement_mag_toggle_on(mag_toggle_time);
      // await this.movement_short_slide(0 + halfline_offset , 350 - halfline_offset , short_move_speed , short_move_time);
      // await this.movement_short_slide(100 - halfline_offset , 350 - halfline_offset , short_move_speed , short_move_time);
      // await this.movement_short_slide(100 , 350 , short_move_speed , short_move_time);
      // await this.movement_mag_toggle_off(mag_toggle_time);
      
    },

    /**
     * @description - This function is used to move the arm to a specific location on the board
     * @param {string} - The location on the board to move to
     * @param {number} - The time it takes for the magnet to turn on
     * @param {number} - The time it takes for the arm to move a short distance
     * @param {number} - The time it takes for the arm to move a long distance
     */
    async yeet_piece(yeet_slot, mag_toggle_time_yeet , short_move_time_yeet , slide_mode_time_yeet){
      console.log('running yeet_piece |' + yeet_slot + "|" +  mag_toggle_time_yeet + "|" + short_move_time_yeet + "|" + slide_mode_time_yeet); //to opease the list gods
      
      //throw piece 
      await this.movement_mag_toggle_off(mag_toggle_time_yeet);
      await this.relative_AN_move('h4' , mag_toggle_time_yeet , short_move_time_yeet , slide_mode_time_yeet);
      await new Promise(resolve => setTimeout(resolve, 1500));
      await this.movement_mag_toggle_on(mag_toggle_time_yeet);
      await this.relative_AN_move("a4" , mag_toggle_time_yeet , short_move_time_yeet , slide_mode_time_yeet);
      await new Promise(resolve => setTimeout(resolve, 300));
      await this.movement_mag_toggle_off(mag_toggle_time_yeet);
    },

    /**
     * @description This function takes a chess cordinate in algebraic notation and returns the corresponding object in the cord_map array
     * @param {string} AN_move - The chess cordinate in algebraic notation
     * @returns {object} - The corresponding object in the cord_map array
     */
    translate_cord_map_to_an(AN_move){
      var AN_move_trans_object = this.cord_map.filter(function(item) {
      return item.chess_cord == AN_move;
      });
      //console.log(AN_move_trans_object)
      return AN_move_trans_object[0]
    },

    translate_num_cord_to_an(x , y){
      var AN_move_trans_object = this.cord_map.filter(function(item) {
        // console.log(item.real_x , " === " , x)
        // console.log(item.real_y , " === " , y)
        // console.log(item.real_x === parseInt(x) && item.real_y === parseInt(y))
      return item.real_x === parseInt(x) && item.real_y === parseInt(y);
      });
      //console.log(AN_move_trans_object[0])
      return AN_move_trans_object[0]
    },

    async relative_probe_check(piece_move_object){
    //   this.mag_toggle_time_slider = 2560
    // this.short_move_time_slider = 500
    // this.long_move_time_slider = 2300
    
      console.log('running relative_probe_check |' + piece_move_object.san); //to opease the list gods
      
      for (let index = 0; index < this.cord_map.length; index++) {
        const cord_map_in = this.cord_map[index];
        if(cord_map_in.chess_cord === piece_move_object.from){
          //console.log(cord_map_in.chess_cord)
          this.move_start = cord_map_in.chess_cord;
        }
        if(cord_map_in.chess_cord === piece_move_object.to){
          //console.log(cord_map_in.chess_cord)
          this.move_end = cord_map_in.chess_cord;
        }
      }

      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      // await this.relative_AN_move(this.move_start , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      // await new Promise(resolve => setTimeout(resolve, 1500));
      // await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
      await this.relative_probe_AN_move(this.move_end , this.mag_toggle_time_slider , this.long_move_time_slider );
      await this.query_moonraker_probe();
      await new Promise(resolve => setTimeout(resolve, 2000));
      if(this.is_scanning){
        console.log("regualr scanning")
        if(this.probe_status == "open"){
          console.log("Probe Open")
        }else{
          console.log("Piece move at relative_probe_check")
          console.log(piece_move_object)
          this.is_scanning = false
          this.check_piece_scanning = false
        }
      }else{
        console.log("I really dont know what you messed up probe check")
      }
      
      // await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      
    },

// This function is used to check if a piece has been captured.
// It does this by moving the probe to the location of the piece,
// then checking if the probe is triggered. If it is not triggered,
// the piece has been captured.
    async relative_probe_check_capture(piece_move_object){
    //   this.mag_toggle_time_slider = 2560
    // this.short_move_time_slider = 500
    // this.long_move_time_slider = 2300
    
      console.log('running relative_probe_check_capture |' + piece_move_object.san); //to opease the list gods
      
      for (let index = 0; index < this.cord_map.length; index++) {
        const cord_map_in = this.cord_map[index];
        if(cord_map_in.chess_cord === piece_move_object.from){
          //console.log(cord_map_in.chess_cord)
          this.move_start = cord_map_in.chess_cord;
        }
        if(cord_map_in.chess_cord === piece_move_object.to){
          //console.log(cord_map_in.chess_cord)
          this.move_end = cord_map_in.chess_cord;
        }
      }

      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      // await this.relative_AN_move(this.move_start , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      // await new Promise(resolve => setTimeout(resolve, 1500));
      // await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
      await this.relative_probe_AN_move(this.move_end , this.mag_toggle_time_slider , this.long_move_time_slider );
      await this.query_moonraker_probe();
      await new Promise(resolve => setTimeout(resolve, 2000));
      if(this.is_scanning){
        console.log("Scanning Possible capture")
        if(this.probe_status == "open"){
          console.log("Probe Open piece captured now check if it was that piece")
          console.log(piece_move_object)
          this.is_scanning = false
          this.check_piece_scanning = false
        }else{
          console.log("Probe Triggered No capture")
          
        }
      }else{
        console.log("I really dont know what you messed up capture check")
      }
      
      // await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      
    },

// This function is used to check if a piece is present at the location of the probe.
// It takes in a chess move object and uses the from and to cordinates to find the 
// corresponding AN cordinates. It then moves the probe to that location and checks if
// the probe is triggered. If it is triggered, it sets the check_piece_scanning flag to false
// and sets the scan_finished flag to true. This will stop the scanning process and return
// the piece found at that location. If no piece is found, it will continue scanning.
/**
 * @description This function is used to check if a piece is in the way of a move
 * @param {object} piece_move_object - This is the move object that is being checked
 * @returns {boolean} - This returns true if the piece is in the way of the move
 */
    async relative_probe_piece_check(piece_move_object){
    //   this.mag_toggle_time_slider = 2560
    // this.short_move_time_slider = 500
    // this.long_move_time_slider = 2300
    
      console.log('running relative_probe_piece_check |' + piece_move_object.san); //to opease the list gods
      
      for (let index = 0; index < this.cord_map.length; index++) {
        const cord_map_in = this.cord_map[index];
        if(cord_map_in.chess_cord === piece_move_object.from){
          //console.log(cord_map_in.chess_cord)
          this.move_start = cord_map_in.chess_cord;
        }
        if(cord_map_in.chess_cord === piece_move_object.to){
          //console.log(cord_map_in.chess_cord)
          this.move_end = cord_map_in.chess_cord;
        }
      }

      await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      // await this.relative_AN_move(this.move_start , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
      // await new Promise(resolve => setTimeout(resolve, 1500));
      // await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
      await this.relative_probe_AN_move(this.move_start , this.mag_toggle_time_slider , this.long_move_time_slider );
      await this.query_moonraker_probe();
      await new Promise(resolve => setTimeout(resolve, 1000));
      if(this.check_piece_scanning){
        console.log("Check Piece scanning")
        if(this.probe_status == "open"){
          console.log("Piece Found at inside probe checl")
          console.log(piece_move_object)
          this.is_scanning = false
          this.check_piece_scanning = false
          this.scan_finished = true;
        }else{
          console.log("Probe Triggered")
          // console.log("Piece Found at")
          // console.log(piece_move_object)
          // this.check_piece_scanning = false
        }
      }else{
        console.log("I really dont know what you messed up piece check")
      }
      
      // await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      
    },

    // async relative_probe_piece_capture_check(piece_move_object){
    // //   this.mag_toggle_time_slider = 2560
    // // this.short_move_time_slider = 500
    // // this.long_move_time_slider = 2300
    
    //   console.log('running relative_probe_piece_check |' + piece_move_object.san); //to opease the list gods
      
    //   for (let index = 0; index < this.cord_map.length; index++) {
    //     const cord_map_in = this.cord_map[index];
    //     if(cord_map_in.chess_cord === piece_move_object.from){
    //       //console.log(cord_map_in.chess_cord)
    //       this.move_start = cord_map_in.chess_cord;
    //     }
    //     if(cord_map_in.chess_cord === piece_move_object.to){
    //       //console.log(cord_map_in.chess_cord)
    //       this.move_end = cord_map_in.chess_cord;
    //     }
    //   }

    //   await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
    //   // await this.relative_AN_move(this.move_start , this.mag_toggle_time_slider , this.long_move_time_slider , this.long_move_time_slider);
    //   // await new Promise(resolve => setTimeout(resolve, 1500));
    //   // await this.movement_mag_toggle_on(this.mag_toggle_time_slider);
    //   await this.relative_probe_AN_move(this.move_start , this.mag_toggle_time_slider , this.long_move_time_slider );
    //   await this.query_moonraker_probe();
    //   await new Promise(resolve => setTimeout(resolve, 1000));
    //   if(this.check_piece_scanning){
    //     console.log("Check Piece scanning for capture")
    //     if(this.probe_status == "open"){
    //       console.log("Piece Found at inside probe checl")
    //       console.log(piece_move_object)
    //       this.check_piece_scanning = false
    //     }else{
    //       console.log("Probe Triggered")
    //       // console.log("Piece Found at")
    //       // console.log(piece_move_object)
    //       // this.check_piece_scanning = false
    //     }
    //   }else{
    //     console.log("I really dont know what you messed up")
    //   }
      
    //   // await this.movement_mag_toggle_off(this.mag_toggle_time_slider);
      
    // },

/*
 * This function is used to move the probe to a relative position on the board.
 * It takes in a string of the form "a1" and translates it into a position on the board.
 * It then moves the probe to that position.
 * 
 * @param AN_move: The string of the form "a1" that represents the position on the board.
 * @param mag_toggle_time: The time in milliseconds that it takes for the magnet to toggle.
 * @param short_move_time: The time in milliseconds that it takes for a short move to complete.
 */
    async relative_probe_AN_move(AN_move, mag_toggle_time , short_move_time ){
      //var move_speed = "F5000";
      var short_move_speed = " F11000";
      // var short_move_speed = "F11000";
      //var slide_move_speed = "F9000";
      //var halfline_offset = 22;
      //var halfline_offset_vertical = 25;
      var AN_move_trans_object = this.translate_cord_map_to_an(AN_move);
      // var obj = JSON.parse(AN_move_trans_objec);
      //console.log('running relative_pawn_move |' + AN_move + "|" +  mag_toggle_time + "|" + short_move_time + "|" + slide_mode_time + "|" + AN_move_trans_object.chess_cord); //to opease the list gods
      await this.movement_short_slide(AN_move_trans_object.send_gcode.out_val_x , AN_move_trans_object.send_gcode.out_val_y + this.offset_y_board_length - this.offset_probe_y , short_move_speed , short_move_time);


    },

    /**
     * @description This function is used to move the marker to a specific location on the board
     * @param {string} AN_move - The chess cordinate of the move
     * @param {number} mag_toggle_time - The time it takes to toggle the magnet
     * @param {number} short_move_time - The time it takes to move the marker a short distance
     * @param {number} slide_mode_time - The time it takes to move the marker a long distance
     */
    async relative_AN_move(AN_move, mag_toggle_time , short_move_time , slide_mode_time){
      //var move_speed = "F5000";
      var short_move_speed = " F11000";
      //var short_move_speed = " F4000";//For Marker Drawing
      // var short_move_speed = "F11000";
      console.log(AN_move)
      console.log(this.translate_cord_map_to_an(AN_move))
      //var slide_move_speed = "F9000";
      //var halfline_offset = 22;
      //var halfline_offset_vertical = 25;
      var AN_move_trans_object = this.translate_cord_map_to_an(AN_move);
      // var obj = JSON.parse(AN_move_trans_objec);
      console.log('running relative_pawn_move |' + AN_move + "|" +  mag_toggle_time + "|" + short_move_time + "|" + slide_mode_time + "|" + AN_move_trans_object.chess_cord); //to opease the list gods
      await this.movement_short_slide(AN_move_trans_object.send_gcode.out_val_x , AN_move_trans_object.send_gcode.out_val_y + this.offset_y_board_length , short_move_speed , short_move_time);


    },

    /**
     * @function draw_clear_square
     * @description This function is used to clear the build plate of any residual material.
     * @param {none}
     * @returns {none}
     */
    async draw_clear_square(){

      var clean_speed = "F15000"
      // G1 X182.071 Y182.071
      this.send_single_gcode("G1 X182.071 Y182.071 F8000");
      await new Promise(resolve => setTimeout(resolve, 3000)); //Let printer move
      this.turn_on_magnet();
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.send_single_gcode("G1 X166.161 Y183.839" + clean_speed);
      this.send_single_gcode("G1 X164.393 Y164.393" + clean_speed);
      this.send_single_gcode("G1 X187.374 Y162.626" + clean_speed);
      this.send_single_gcode("G1 X189.142 Y189.142" + clean_speed);
      this.send_single_gcode("G1 X159.090 Y190.910" + clean_speed);
      this.send_single_gcode("G1 X157.322 Y157.322" + clean_speed);
      this.send_single_gcode("G1 X194.445 Y155.555" + clean_speed);
      this.send_single_gcode("G1 X196.213 Y196.213" + clean_speed);
      this.send_single_gcode("G1 X152.019 Y197.981" + clean_speed);
      this.send_single_gcode("G1 X150.251 Y150.251" + clean_speed);
      this.send_single_gcode("G1 X201.517 Y148.483" + clean_speed);
      this.send_single_gcode("G1 X203.284 Y203.284" + clean_speed);
      this.send_single_gcode("G1 X144.948 Y205.052" + clean_speed);
      this.send_single_gcode("G1 X144.948 Y205.052" + clean_speed);
      this.send_single_gcode("G1 X143.180 Y143.180" + clean_speed);
      this.send_single_gcode("G1 X208.588 Y141.412" + clean_speed);
      this.send_single_gcode("G1 X210.355 Y210.355" + clean_speed);
      this.send_single_gcode("G1 X137.877 Y212.123" + clean_speed);
      this.send_single_gcode("G1 X136.109 Y136.109" + clean_speed);
      this.send_single_gcode("G1 X215.659 Y134.341" + clean_speed);
      this.send_single_gcode("G1 X217.426 Y217.426" + clean_speed);
      this.send_single_gcode("G1 X130.806 Y219.194" + clean_speed);
      this.send_single_gcode("G1 X129.038 Y129.038" + clean_speed);
      this.send_single_gcode("G1 X222.730 Y127.270" + clean_speed);
      this.send_single_gcode("G1 X224.497 Y224.497" + clean_speed);
      this.send_single_gcode("G1 X123.735 Y226.265" + clean_speed);
      this.send_single_gcode("G1 X121.967 Y121.967" + clean_speed);
      this.send_single_gcode("G1 X229.801 Y120.199" + clean_speed);
      this.send_single_gcode("G1 X231.569 Y231.569" + clean_speed);
      this.send_single_gcode("G1 X116.664 Y233.336" + clean_speed);
      this.send_single_gcode("G1 X114.896 Y114.896" + clean_speed);
      this.send_single_gcode("G1 X236.872 Y113.128" + clean_speed);
      this.send_single_gcode("G1 X238.640 Y238.640" + clean_speed);
      this.send_single_gcode("G1 X109.593 Y240.407" + clean_speed);
      this.send_single_gcode("G1 X107.825 Y107.825" + clean_speed);
      this.send_single_gcode("G1 X243.943 Y106.057" + clean_speed);
      this.send_single_gcode("G1 X245.711 Y245.711" + clean_speed);
      this.send_single_gcode("G1 X102.522 Y247.478" + clean_speed);
      this.send_single_gcode("G1 X100.754 Y100.754" + clean_speed);
      this.send_single_gcode("G1 X251.014 Y98.986" + clean_speed);
      this.send_single_gcode("G1 X252.782 Y252.782" + clean_speed);
      this.send_single_gcode("G1 X95.450 Y254.550" + clean_speed);
      this.send_single_gcode("G1 X93.683 Y93.683" + clean_speed);
      this.send_single_gcode("G1 X258.085 Y91.915" + clean_speed);
      this.send_single_gcode("G1 X259.853 Y259.853" + clean_speed);
      this.send_single_gcode("G1 X88.379 Y261.621" + clean_speed);
      this.send_single_gcode("G1 X86.612 Y86.612" + clean_speed);
      this.send_single_gcode("G1 X265.156 Y84.844" + clean_speed);
      this.send_single_gcode("G1 X266.924 Y266.924" + clean_speed);
      this.send_single_gcode("G1 X81.308 Y268.692" + clean_speed);
      this.send_single_gcode("G1 X79.541 Y79.541" + clean_speed);
      this.send_single_gcode("G1 X272.227 Y77.773" + clean_speed);
      this.send_single_gcode("G1 X273.995 Y273.995" + clean_speed);
      this.send_single_gcode("G1 X74.237 Y275.763" + clean_speed);
      this.send_single_gcode("G1 X72.470 Y72.470" + clean_speed);
      this.send_single_gcode("G1 X279.298 Y70.702" + clean_speed);
      this.send_single_gcode("G1 X281.066 Y281.066" + clean_speed);
      this.send_single_gcode("G1 X67.166 Y282.834" + clean_speed);
      this.send_single_gcode("G1 X65.398 Y65.398" + clean_speed);
      this.send_single_gcode("G1 X286.369 Y63.631" + clean_speed);
      this.send_single_gcode("G1 X288.137 Y288.137" + clean_speed);
      this.send_single_gcode("G1 X60.095 Y289.905" + clean_speed);
      this.send_single_gcode("G1 X58.327 Y58.327" + clean_speed);
      this.send_single_gcode("G1 X293.440 Y56.560" + clean_speed);
      this.send_single_gcode("G1 X295.208 Y295.208" + clean_speed);
      this.send_single_gcode("G1 X53.024 Y296.976" + clean_speed);
      this.send_single_gcode("G1 X51.256 Y51.256" + clean_speed);
      this.send_single_gcode("G1 X300.511 Y49.489" + clean_speed);
      this.send_single_gcode("G1 X302.279 Y302.279" + clean_speed);
      this.send_single_gcode("G1 X45.953 Y304.047" + clean_speed);
      this.send_single_gcode("G1 X44.185 Y44.185" + clean_speed);
      this.send_single_gcode("G1 X307.583 Y42.417" + clean_speed);
      this.send_single_gcode("G1 X309.350 Y309.350" + clean_speed);
      this.send_single_gcode("G1 X38.882 Y311.118" + clean_speed);
      this.send_single_gcode("G1 X37.114 Y37.114" + clean_speed);
      this.send_single_gcode("G1 X314.654 Y35.346" + clean_speed);
      this.send_single_gcode("G1 X316.421 Y316.421" + clean_speed);
      this.send_single_gcode("G1 X31.811 Y318.189" + clean_speed);
      this.send_single_gcode("G1 X30.043 Y30.043" + clean_speed);
      this.send_single_gcode("G1 X321.725 Y28.275" + clean_speed);
      this.send_single_gcode("G1 X323.492 Y323.492" + clean_speed);
      this.send_single_gcode("G1 X24.740 Y325.260" + clean_speed);
      this.send_single_gcode("G1 X22.972 Y22.972" + clean_speed);
      this.send_single_gcode("G1 X328.796 Y21.204" + clean_speed);
      this.send_single_gcode("G1 X330.563 Y330.563" + clean_speed);
      this.send_single_gcode("G1 X17.669 Y332.331" + clean_speed);
      this.send_single_gcode("G1 X15.901 Y15.901" + clean_speed);
      this.send_single_gcode("G1 X335.867 Y14.133 F8000");

      // this.send_single_gcode("G1  F8000");
    },

    /**
     * @description This function is used to send a single gcode command to the printer
     * @param {string} gcode_command - The gcode command to be sent to the printer
     */
    async draw_smile() {
      //GCODE FOR SMILE
    // T1 M6
    // G90  //set relative
    // G54 X0 Y0
    // G00 X0 Y0 
    // G00 X-25 Y20
    // G91 X-10 
    // G02 X10 Y-10 I10 J0 F200 M3
    // G02 X-10 Y10 I0 J10;
    // G90 G00 M5 X0 Y0;
    // G00 X25 Y20
    // G91 X-10 
    // G02 X10 Y-10 I10 J0 F200M3
    // G02 X-10 Y10 I0 J10;
    // G90 G00 M5 X0 Y0;
    // G00 X40 Y0
    // G02 X-40 Y0 I-40 J0 F200 M3
    // G90 G00 M5 X-55 Y0;
    // G02 X0 Y-55 I55 J0 F200 M3
    // G02 X-55 Y0 I0 J55
    // M30;

    //Klipper GCODE
    // var multi_gcode_obj = {};
    // G90
    // G1 X150 Y150
    // timeout(ms) {
    // return new Promise(resolve => setTimeout(resolve, ms));
    // },
    // async sleep(fn, ...args) {
    //       await timeout(3000);
    //       return fn(...args);
    // },
      // G1 X87.5 Y218.75 F6000
      // G1 X43.75 Y131.25 F6000
      // G1 X87.5 Y87.5 F6000
      // G1 X175 Y87.5 F6000
      // G1 X218.75 Y131.25 F6000
      // G1 X175 Y218.75 F6000

      // async function sleep(fn, ...args) {
      //     await timeout(3000);
      //     return fn(...args);
      // }

      // console.log("In 1");
      // await new Promise(resolve => setTimeout(resolve, 1000));

      this.send_single_gcode('G1 X87.5 Y218.75 F6000'); //left eye
      await new Promise(resolve => setTimeout(resolve, 3000));
      this.turn_on_magnet();
      await new Promise(resolve => setTimeout(resolve, 2000));
      this.turn_off_magnet();
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.send_single_gcode('G1 X43.75 Y131.25 F6000'); //right face start
      await new Promise(resolve => setTimeout(resolve, 3000));
      this.turn_on_magnet();
      await new Promise(resolve => setTimeout(resolve, 1000));
      this.send_single_gcode('G1 X87.5 Y87.5 F6000');
      this.send_single_gcode('G1 X175 Y87.5 F6000');
      this.send_single_gcode('G1 X218.75 Y131.25 F6000');
      await new Promise(resolve => setTimeout(resolve, 2200));
      this.turn_off_magnet();
      this.send_single_gcode('G1 X175 Y218.75 F6000'); //right eye
      await new Promise(resolve => setTimeout(resolve, 3000));
      this.turn_on_magnet();
      await new Promise(resolve => setTimeout(resolve, 2000));
      this.turn_off_magnet();
    },

    /**
     * @description This function is used to home the printer in the y direction
     * @param {string} send_code1 - The gcode command to home the printer in the y direction
     * @param {string} send_code2 - The gcode command to home the printer in the x direction
     * @returns {void}
     */
    home_xy(){
      var send_code1 = 'G28 Y';
      var send_code2 = 'G28 X';
      axios({
        method: "post",
        url: "http://192.168.1.5/printer/gcode/script?script=" + send_code1,
        //data: bodyFormData,
        //headers: { "Content-Type": "multipart/form-data" },
      })
        .then(function (response) {
          //handle success
          console.log(response);
        })
        .catch(function (response) {
          //handle error
          console.log(response);
        });
      axios({
        method: "post",
        url: "http://192.168.1.5/printer/gcode/script?script=" + send_code2,
        //data: bodyFormData,
        //headers: { "Content-Type": "multipart/form-data" },
      })
        .then(function (response) {
          //handle success
          console.log(response);
        })
        .catch(function (response) {
          //handle error
          console.log(response);
        });
    },

    send_multi_gcode(multi_gcode_obj) {
      console.log(multi_gcode_obj);
      var send_code = '';
      axios({
        method: "post",
        url: "http://192.168.1.5/printer/gcode/script?script=" + send_code,
        //data: bodyFormData,
        //headers: { "Content-Type": "multipart/form-data" },
      })
        .then(function (response) {
          //handle success
          console.log(response);
        })
        .catch(function (response) {
          //handle error
          console.log(response);
        });
    },

    send_loop() {
      axios({
        method: "post",
        url: "http://192.168.1.5/printer/gcode/script?script=" + `
        SET_HEATER_TEMPERATURE HEATER=my_generic_heater TARGET=100;
        `,
        //data: bodyFormData,
        //headers: { "Content-Type": "multipart/form-data" },
      })
        .then(function (response) {
          //handle success
          console.log(response);
          axios({
            method: "post",
            url: "http://192.168.1.5/printer/gcode/script?script=" + `
            G1 X80 Y80.00 F6000;
            `,
            //data: bodyFormData,
            //headers: { "Content-Type": "multipart/form-data" },
          })
            .then(function (response) {
              //handle success
              console.log(response);
              axios({
                method: "post",
                url: "http://192.168.1.5/printer/gcode/script?script=" + `
                G1 X80 Y270.00 F6000;
                `,
                //data: bodyFormData,
                //headers: { "Content-Type": "multipart/form-data" },
              })
                .then(function (response) {
                  //handle success
                  console.log(response);
                  axios({
                    method: "post",
                    url: "http://192.168.1.5/printer/gcode/script?script=" + `
                    G1 X270 Y270.00 F6000;
                    `,
                    //data: bodyFormData,
                    //headers: { "Content-Type": "multipart/form-data" },
                  })
                    .then(function (response) {
                      //handle success
                      console.log(response);
                      axios({
                        method: "post",
                        url: "http://192.168.1.5/printer/gcode/script?script=" + `
                        G1 X270 Y80.00 F6000;
                        `,
                        //data: bodyFormData,
                        //headers: { "Content-Type": "multipart/form-data" },
                      })
                        .then(function (response) {
                          //handle success
                          console.log(response);
                        })
                        .catch(function (response) {
                          //handle error
                          console.log(response);
                        });
                    })
                    .catch(function (response) {
                      //handle error
                      console.log(response);
                    });
                })
                .catch(function (response) {
                  //handle error
                  console.log(response);
                });
            })
            .catch(function (response) {
              //handle error
              console.log(response);
            });
        })
        .catch(function (response) {
          //handle error
          console.log(response);
        });
        setTimeout(() => {
          axios({
            method: "post",
            url: "http://192.168.1.5/printer/gcode/script?script=" + `
            SET_HEATER_TEMPERATURE HEATER=my_generic_heater TARGET=0;
            `,
            //data: bodyFormData,
            //headers: { "Content-Type": "multipart/form-data" },
          })
            .then(function (response) {
              //handle success
              console.log(response);
            })
            .catch(function (response) {
              //handle error
              console.log(response);
            }); 
          }, 8000);
    },

    undo() {
      this.game.undo()
      this.board.set({fen: this.game.fen()})
    },

    userPlay() {
      return async (orig, dest) => {
        //console.log("Piece Was moved from " , orig , ":" ,dest)

        this.is_scanning = false;
        this.check_piece_scanning = false;

        // console.log(this.game);
        // console.log(this.board);
        // console.log(this.game.fen());
        // console.log(this.board.getFen());
        // console.log(this.possibleMoves());
        // console.log(this.game.moves({verbose: true}));
        if (this.isPromotion(orig, dest)) {
          this.promoteTo = this.onPromotion()
        }
        //console.log(this.game.moves({verbose: true}));
        // var piece_moved = this.game.moves({verbose: true})
        //   .filter((move) => orig == move)
          // .map((move) => move.san)
        var piece_moved = this.game.moves({verbose: true}).filter(function(item) {
        return item.from == orig && item.to == dest;
        });
        
        console.log(piece_moved[0])

        if(this.move_pieces_toggle){
          await this.AN_move_router(piece_moved[0]);
        }
        // console.log(piece_moved[0].piece + dest);
        // console.log(piece_moved[0].san);
        //console.log(piece_moved);
        // this.AN_move_router(piece_moved[0].san , orig , dest , piece_moved[0].piece , piece_moved[0].color);
        // const get_legal_moves_by_piece = (game, piece) => {
        //   return game.moves({ verbose: true })
        //               .filter((move) => move.piece === piece.type && move.color === piece.color)
        //               .map((move) => move.san)
        // }
        // console.log(piece_moved.piece)
        this.game.move({from: orig, to: dest, promotion: this.promoteTo}) // promote to queen for simplicity
        this.board.set({
          fen: this.game.fen()
        })
        this.current_fen = this.game.fen()
        this.calculatePromotions()
        this.aiNextMove()
        this.board.setShapes([{orig: 'a1', brush: 'red'}]);
        this.paintThreats();
        this.scan_targets = this.game.moves({verbose: true}); //{verbose: true}
        //console.log(this.board)
        this.board_update_tick()
      };
    },

    async scanned_user_move(orig, dest){
        if (this.isPromotion(orig, dest)) {
          this.promoteTo = this.onPromotion()
        }

        // var piece_moved = this.game.moves({verbose: true}).filter(function(item) {
        // return item.from == orig && item.to == dest;
        // });
        
        // console.log(piece_moved[0])

        // if(this.move_pieces_toggle){
        //   await this.AN_move_router(piece_moved[0]);
        // }

        this.game.move({from: orig, to: dest, promotion: this.promoteTo}) // promote to queen for simplicity
        this.board.set({
          fen: this.game.fen()
        })
        this.current_fen = this.game.fen()
        this.calculatePromotions()
        this.aiNextMove()
        this.board.setShapes([{orig: 'a1', brush: 'red'}]);
        this.paintThreats();
        this.scan_targets = this.game.moves({verbose: true}); //{verbose: true}
        //console.log(this.board)
        this.board_update_tick()
    },

    async aiNextMove() {
      //console.log(this.game.moves({verbose: true}));
      //let moves = this.game.moves({verbose: true})
      //console.log(moves)
      //let randomMove = moves[Math.floor(Math.random() * moves.length)]
      let stockfish_best_move = {};

      //console.log(this.current_fen)
      //run Stockfish
      await axios({
        method: "get",
        url: "http://localhost:3000/stockfish_evals/" + encodeURIComponent(this.current_fen), //+ encodeURI(this.current_fen)
        //data: bodyFormData,
        //headers: { "Content-Type": "multipart/form-data" },
      })
        .then(function (response) {
          //handle success
          stockfish_best_move = response.data[0].best_move /////YOU NEED TO PARSE THE MOVE INTO FROM: and TO:
          if(stockfish_best_move.includes("x")){
            console.log("Code in takes");
            return
          }
          // var regex_best_move = stockfish_best_move.best_move.split()
          var from = stockfish_best_move[0] + stockfish_best_move[1]
          var to = stockfish_best_move[2] + stockfish_best_move[3]
          stockfish_best_move = {'from': from, 'to': to}
          //console.log(stockfish_best_move + "|" + from + "|" + to)
          //console.log(response);
        })
        .catch(function (response) {
          //handle error
          console.log(response);
        });

      //console.log(randomMove);
      //console.log(stockfish_best_move)

      var piece_moved = this.game.moves({verbose: true}).filter(function(item) {
      return item.from == stockfish_best_move.from && item.to == stockfish_best_move.to;
      });
      if(this.move_pieces_toggle){
          await this.AN_move_router(piece_moved[0]);
        }

      this.game.move(stockfish_best_move)

      this.board.set({
        fen: this.game.fen(),
        turnColor: this.toColor(),
        showThreats: true,
        movable: {
          color: this.toColor(),
          dests: this.possibleMoves(),
          events: { after: this.userPlay()},
        }
      });
      this.board.setShapes([{orig: 'a1', brush: 'red'}]);
      this.paintThreats();
      this.scan_targets = this.game.moves({verbose: true}); //{verbose: true}
      this.board_update_tick()
      // stockfish_best_move.to
      // this.send_light_midi()
      this.last_trans_cord = this.translate_cord_map_to_an(stockfish_best_move.to).real_y.toString() + this.translate_cord_map_to_an(stockfish_best_move.to).real_x.toString()
        //console.log(trans_cord.real_x.toString() + trans_cord.real_y.toString())
      
      this.board_update_tick()
        // if (stockfish_best_move.san.includes("x")){
        //   this.send_light_midi([144 , trans_cord , 4])
        // }else{
        //   this.send_light_midi([144 , trans_cord , 15])
        // }

      // this.target_list_piece_moved = this.game.moves({verbose: true}).filter(function(item) {
      //   return  item.to == current_scan_location; //Dont return duplicate .to
      //   });

      // this.scan_targets_filtered.filter((v,i,a)=>a.findIndex(v2=>(v2.id===v.id))===i)


      // Keep any san that has x
      var to_array = [];
      var filter_target_hold = [];
      // var found_flag = false;
      // var that = this;
      for (let index = 0; index < this.scan_targets.length; index++) {
          const scan_position = this.scan_targets[index];
          if (scan_position.san.includes("x")){
            filter_target_hold.push(scan_position);
            to_array.push(scan_position.to);
          }
          to_array.push(scan_position.to);
      }

      var uniq_to_array = [...new Set(to_array)];

      //console.log(uniq_to_array)

      for (let index1 = 0; index1 < uniq_to_array.length; index1++) {
        for (let index2 = 0; index2 < this.scan_targets.length; index2++) {
          const scan_position = this.scan_targets[index2];
          if(scan_position.to === to_array[index1]){
            //console.log("True at ", scan_position.to , "|" ,  to_array[index1])
            filter_target_hold.push(scan_position);
            break;
          }
        }
      }

      // for (let index = 0; index < this.scan_targets.length; index++) {
      //   const scan_position = this.scan_targets[index];
      //   if (substrings.some(v => str.includes(v))) {

      //   }
    // There's at least one
// }
//       }

      // for (let index1 = 0; index1 < to_array.length; index1++) {
      //   for (let index2 = 0; index2 < this.scan_targets.length; index2++) {
      //     const scan_position = this.scan_targets[index2];
      //     if(scan_position.to === to_array[index1]){
      //       console.log("True at ", scan_position.to , "|" ,  to_array[index1])
      //       break
      //     }else{
      //       filter_target_hold.push(scan_position);
      //       break;
      //     }
      //     // if(scan_position.to === to_array[index1]){
      //     //   filter_target_hold.push(scan_position);
      //     // }
      //   }
      // }
      //console.log(to_array)


      // for (let index = 0; index < this.scan_targets.length; index++) {
      //     const scan_position = this.scan_targets[index];
      //     if (scan_position.san.includes("x")){
      //       filter_target_hold.push(scan_position);
      //       to_array.push(scan_position.to);
      //       console.log()
      //     }else{
      //       for (let index = 0; index < to_array.length; index++) {
      //         if(scan_position.to === to_array[index]){
      //           console.log("Already Added")
      //           found_flag = false;
      //         }else{
      //           found_flag = true;
      //         }
      //         if(found_flag){
      //           filter_target_hold.push(scan_position);
      //           to_array.push(scan_position.to);
      //           found_flag = false;
      //         }
      //       }
      //       // if(scan_position.to === forloop_to_array){
      //       //   break;
      //       // }else{
      //       //   filter_target_hold.push(scan_position);
      //       //   to_array.push(scan_position.to);
      //       // }
      //       // for (let index = 0; index < to_array.length; index++) {
      //       //   const element = to_array[index];
      //       //   console.log(element)
      //       //   console.log(typeof(element))
      //       //   console.log(scan_position.to)
      //       //   console.log(typeof(scan_position.to))
      //       //   console.log(element === scan_position.to)
      //       //   console.log(to_array)
      //       //   if(!(element === scan_position.to)){
      //       //     break;
      //       //   }else{
      //       //     filter_target_hold.push(scan_position);
      //       //     to_array.push(scan_position.to);
      //       //   }
      //       // }
      //     }
      //     found_flag = false;
      // }

      this.scan_targets_filtered = filter_target_hold

      // console.log("CURRENT TARGETS")
      // console.log(this.scan_targets_filtered)
      // console.log(this.scan_targets)

      // console.log("to_array: ")
      // console.log(to_array)

      //this.scan_targets_filtered = this.scan_targets

      if(!this.disable_scanning){
        this.is_scanning = true
        this.scan_finished = false;
      while(this.is_scanning){
        for (let index = 0; index < this.scan_targets.length; index++) {
          const scan_position = this.scan_targets[index];
          if(this.is_scanning){
            console.log("Starting scanning Loop")
            if (scan_position.san.includes("x")){
              this.current_scan_square = scan_position;
              await this.relative_probe_check_capture(scan_position)
              console.log("Finished Capture Move scan of: "+  scan_position.to + "|" + scan_position.from)
              //break //curently trying to stop prob check from working when first capture

              //IF piece is moved and finds move before check all pieces it will assume that the capture move has been performed
              //Needed to check other capture moves post move to ensure this isnt the case
            }else{
              this.current_scan_square = scan_position;
              await this.relative_probe_check(scan_position)
              console.log("Finished scan of: "+  scan_position.to + "|" + scan_position.from)
            }
        
          }else{
            break;
          }
          
        }
      }
      this.check_piece_scanning = true
      //var target_list_check_piece = {}
      var current_scan_location = this.current_scan_square.to
      this.target_list_piece_moved = this.game.moves({verbose: true}).filter(function(item) {
        return  item.to == current_scan_location;
        });

      if(this.target_list_piece_moved.length <= 1){
        console.log("Found Move one option")
        console.log(this.current_scan_square)
        this.scan_finished = true
        this.check_piece_scanning = false
        if(this.target_list_piece_moved[0].san.includes("x")){
          await this.strip_san_finish_capture(this.target_list_piece_moved[0]);
        }
      }else{
      while(this.check_piece_scanning){
        for (let index = 0; index < this.target_list_piece_moved.length; index++) {
          const scan_position = this.target_list_piece_moved[index];

            if(this.check_piece_scanning){
              if(scan_position.san.includes("x")){
              //check which piece was moved
              console.log("Move capoture piece now")
              console.log(scan_position)
              this.current_scan_square = scan_position;
              await this.relative_probe_piece_check(scan_position)
              }else{
                console.log(scan_position)
                this.current_scan_square = scan_position;
                await this.relative_probe_piece_check(scan_position)
              }
            }
            
            // if(scan_position.to == this.current_scan_square.to)
            // console.log(scan_position)
            // this.current_scan_square = scan_position;
            // await this.relative_probe_piece_check(scan_position)
            // if (scan_position.san.includes("x")){
            //   await this.relative_probe_piece_capture_check(scan_position)
            // }else{
            //   await this.relative_probe_piece_check(scan_position)
            // }
          
        }
      }
      }
      if(!this.scan_finished){
        console.log("Scan was stopped by piece move")
      }else{
        console.log("Found Move After")
      console.log(this.current_scan_square)
      this.scanned_user_move(this.current_scan_square.from, this.current_scan_square.to)
      console.log("Yolo gottum")
      }
      }
      
    },

    sendMessage() {
      console.log(this.connection);
      var json_rpc = JSON.stringify({
          "jsonrpc": "2.0",
          "method": "server.connection.identify",
          "params": {
              "client_name": "Mainsail",
              "version": "2.2.1",
              "type": "web",
              "url": "http://localhost:8080"
          },
          "id": 4656,
      })
      this.connection.send(json_rpc);
    },

    async query_moonraker_probe(){
      var json_rpc = JSON.stringify({"jsonrpc":"2.0","method":"printer.gcode.script","params":{"script":"QUERY_PROBE"},"id":6969})
      await this.connection.send(json_rpc);
    },

  },
  mounted() {
    this.board.set({
      movable: { events: { after: this.userPlay()} },
    })
    this.mag_toggle_time_slider = 2500
    this.short_move_time_slider = 900
    this.long_move_time_slider = 2500

    // if (navigator.requestMIDIAccess) {
    //     navigator.requestMIDIAccess({
    //         sysex: true
    //     }).then(onMIDISuccess, onMIDIFailure);
    // } else {
    //     alert("No MIDI support in your browser.");
    // }


    //this.$refs.navigator.requestMIDIAccess().then(this.onMIDISuccess, this.onMIDIFailure)
    if (typeof navigator.requestMIDIAccess !== "undefined") {
        console.log("Trying Nav Access")
        navigator.requestMIDIAccess({sysex: true}).then(this.onMIDISuccess, this.onMIDIFailure)
    } else {
        console.log('MIDI not available');
    }
  },
  created() {
    // this.$socket.onOpen = () => {
    //   console.log('socket connected')
    // }
    // this.$socket.onMessage = (msg) => {
    //   console.log(msg)
    // }
    // this.$socket.onClose = (msg) => {
    //   console.log('socket closed' + msg)
    // }
    // this.$socket.onError = (msg) => {
    //   console.log('socket error' + msg)
    // }
    var that = this;

    console.log("Starting connection to WebSocket Server")
    this.connection = new WebSocket("ws://192.168.1.5/websocket")

    console.log("This is after the conn is made")

    this.connection.onmessage = function(event) {
      //console.log(JSON.parse(event.data));
      var parsed_message = JSON.parse(event.data);
      //console.log(parsed_message)
      if(parsed_message.method == 'notify_gcode_response'){
        that.probe_status = parsed_message.params[0].substring(10)
        console.log(parsed_message.params[0].substring(10))

      }

      if(parsed_message.result){
        //console.log(parsed_message.result.connection_id)

        // if(parsed_message.id == 6969){
        //   console.log(parsed_message.result)
        // }

        if(parsed_message.result.connection_id){
          that.moonraker_conn_id = parsed_message.result.connection_id
        }else{
          console.log(parsed_message)
        }
        //that.$nextTick();
        // that.moonraker_conn_id = parsed_message.result.connection_id
        //that.$nextTick();
      }
    }

    this.connection.onopen = function(event) {
      console.log(event)
      console.log("Successfully connected to the echo websocket server...")
      that.sendMessage();
    }

    bus.$on('undo', () => {
      this.undo()
    })
  },
  // watch(){
  //   index(newValue, oldValue){
  //     console.log("Change Detected: ",newValue , "|" , oldValue )
  //     // here you can do whatever you want
  //   }
  // },
}
</script>
